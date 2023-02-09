<script>
import BusinessForm from "./components/BusinessForm.vue";
import ClientForms from "./components/ClientForms.vue";
import GoodsForm from "./components/GoodsForm.vue";
import NotificationBar from "./components/NotificationBar.vue";
import InvoicePreview from "./components/InvoicePreview.vue";
import html2canvas from "html2canvas";
import jsPDF from "jspdf";

export default {
  components: {
    BusinessForm,
    ClientForms,
    GoodsForm,
    NotificationBar,
    InvoicePreview,
  },
  data() {
    return {
      businessDetails: {},
      clientDetails: {},
      transaction: {
        date: "",
        No: "",
        currency: "",
      },
      goods: "",
      businessForm: true,
      clientForm: false,
      goodsForm: false,
      businessFormBtn: "active",
      clientFormBtn: "",
      goodsFormBtn: "",
      notifyShow: false,
      notify: {
        message: "",
        class: "",
      },
    };
  },
  methods: {
    makePDF() {
      window.html2canvas = html2canvas;
      let doc = new jsPDF("p", "pt", "a4");
      doc.html(document.querySelector("#print-invoice"), {
        callback: function (pdf) {
          pdf.save("invoice.pdf");
        },
      });
    },

    showNotifyBar(message, classL) {
      this.notifyShow = true;
      this.notify.message = message;
      this.notify.class = classL;

      setTimeout(() => {
        this.notifyShow = false;
      }, 3000);
    },
    businessShow() {
      this.businessForm = true;
      this.clientForm = false;
      this.goodsForm = false;
      this.businessFormBtn = "active";
      this.clientFormBtn = "";
      this.goodsFormBtn = "";
    },
    clientShow() {
      this.businessForm = false;
      this.clientForm = true;
      this.goodsForm = false;
      this.businessFormBtn = "";
      this.clientFormBtn = "active";
      this.goodsFormBtn = "";
    },
    goodShow() {
      this.businessForm = false;
      this.clientForm = false;
      this.goodsForm = true;
      this.businessFormBtn = "";
      this.clientFormBtn = "";
      this.goodsFormBtn = "active";
    },
    addBusiness(name) {
      this.businessDetails = name;
      this.clientShow();
      this.showNotifyBar(
        `welcome ${this.businessDetails.name}, your details has been added.`,
        "notification-bar success"
      );
    },
    addClient(name) {
      this.ClientDetails = name;
      this.goodShow();
      this.showNotifyBar("Client added.", "notification-bar success");
    },
    addGood(item) {
      this.goods = [...this.goods, item];
      this.showNotifyBar(
        "Item added Successfully.",
        "notification-bar success"
      );
    },
    removeGood(id) {
      this.goods = this.goods.filter((item) => item.id !== id);
    },
    generateInvoice() {
      if (!this.goods) {
        this.showNotifyBar("No items to add.", "notification-bar error");
      } else {
        this.storeLS();
        this.showNotifyBar(
          "Your Invoice is loading.",
          "notification-bar success"
        );
      }
    },
    noFill() {
      this.showNotifyBar("Please Input Details.", "notification-bar error");
    },
    storeLS() {
      //   storing to local storage
      localStorage.setItem(
        "Business Details",
        JSON.stringify(this.businessDetails)
      );
      localStorage.setItem(
        "Client Details",
        JSON.stringify(this.clientDetails)
      );
      localStorage.setItem("Goods Items", JSON.stringify(this.goods));
    },
  },
};
</script>

<template>
  <h1 class="logo">PayEvi</h1>

  <NotificationBar v-show="notifyShow" :notify="notify" />

  <main>
    <section>
      <div class="form-container">
        <div class="form-btns">
          <div :class="[businessFormBtn]" @click="businessShow">
            Business Details
          </div>
          <div :class="[clientFormBtn]" @click="clientShow">
            Client's Details
          </div>
          <div :class="[goodsFormBtn]" @click="goodShow">Goods Details</div>
        </div>
        <BusinessForm
          @add-business="addBusiness"
          @no-fill="noFill"
          v-show="businessForm"
        />

        <ClientForms
          @add-client="addClient"
          @to-business="businessShow()"
          @no-fill="noFill"
          v-show="clientForm"
        />

        <GoodsForm
          :goods="goods"
          v-show="goodsForm"
          @add-good="addGood"
          @no-fill="noFill"
          @generate-invoice="generateInvoice()"
          @to-client="clientShow()"
          @remove-good="removeGood"
        />
      </div>
    </section>

    <div class="preview">
      <div class="invoice-preview">
        <InvoicePreview class="invoice-generated" />
      </div>
      <div class="btn-right">
        <button @click="makePDF">Download PDF</button>
      </div>
    </div>
  </main>
</template>

<style scoped>
.invoice-generated {
  height: fit-content;
}
</style>
