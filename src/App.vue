<script>
import BusinessForm from "./components/BusinessForm.vue";
import ClientForms from "./components/ClientForms.vue";
import GoodsForm from "./components/GoodsForm.vue";
import NotificationBar from "./components/NotificationBar.vue";
import InvoicePreview from "./components/InvoicePreview.vue";
import Loading from "./components/Loading.vue";
import html2canvas from "html2canvas";
import jsPDF from "jspdf";

export default {
  components: {
    BusinessForm,
    ClientForms,
    GoodsForm,
    NotificationBar,
    Loading,
    InvoicePreview,
  },
  data() {
    return {
      businessDetails: {},
      clientDetails: {},
      invoice: {},
      isGenerated: false,
      goods: [],
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
      let doc = new jsPDF("p", "pt", "a4", true);
      doc.html(document.querySelector("#print-invoice"), {
        callback: function (pdf) {
          pdf.save("invoice.pdf");
        },
      });
    },

    showNotifyBar(message, classL) {
      this.notifyShow = false;
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
      this.clientDetails = name;
      this.goodShow();
      this.showNotifyBar("Client added.", "notification-bar success");
      console.log("clientDetails:", this.clientDetails);
      console.log("client:", name.name);
    },
    addGood(item) {
      this.goods = [...this.goods, item];
      this.showNotifyBar(
        "Item added Successfully.",
        "notification-bar success"
      );
      this.newGoods = this.goods;
    },
    addInv(name) {
      this.invoice = name;
    },
    removeGood(id) {
      this.goods = this.goods.filter((item) => item.id !== id);
      this.showNotifyBar(
        "Item removed Successfully.",
        "notification-bar error"
      );
      this.newGoods = this.goods;
    },
    generateInvoice() {
      if (!this.goods) {
        this.showNotifyBar("No items to add.", "notification-bar error");
      } else {
        this.showNotifyBar(
          "Your Invoice is loading.",
          "notification-bar success"
        );
      }
      setTimeout(() => {
        this.isGenerated = true;
      }, 3000);
    },
    noFill() {
      this.showNotifyBar("Please Input Details.", "notification-bar error");
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
          @add-inv="addInv"
          @generate-invoice="generateInvoice()"
          @to-client="clientShow()"
          @remove-good="removeGood"
        />
      </div>
    </section>

    <div class="preview">
      <div class="invoice-preview">
        <div class="invoice-generated">
          <Loading v-show="!isGenerated" />
          <InvoicePreview
            v-show="isGenerated"
            :invoice="invoice"
            :generated="isGenerated"
            :businessDetails="businessDetails"
            :clientDetails="clientDetails"
            :goods="goods"
          />
        </div>
      </div>
      <div v-show="isGenerated" class="btn-right btn-top">
        <button @click="makePDF">Download PDF</button>
      </div>
    </div>
  </main>
</template>

<style scoped></style>
