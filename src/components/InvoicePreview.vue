<template>
  <aside id="print-invoice">
    <header>
      <div class="business-details">
        <h2>{{ businessDetails.name }}</h2>
        <p>{{ businessDetails.description }}</p>
        <p>{{ businessDetails.number }}</p>
      </div>
      <h1>INVOICE</h1>
    </header>

    <div class="container">
      <div class="head">
        <div class="client-details">
          <b>BILL TO:</b>
          <h3>{{ clientDetails.name }}</h3>
          <p>{{ clientDetails.address }}</p>
          <p>{{ clientDetails.number }}</p>
        </div>
        <div class="invoice-details">
          <div class="inv-row">
            <b>INVOICE NO:</b>
            <p>EMDES0012</p>
          </div>
          <div class="inv-row">
            <b>DATE:</b>
            <p>07/02/2023</p>
          </div>
        </div>
      </div>

      <table>
        <thead>
          <tr>
            <th>S/N</th>
            <th>Description</th>
            <th>Quantity</th>
            <th>Rate</th>
            <th>Amount (&#8358)</th>
          </tr>
        </thead>
        <tbody>
          
        <tr v-for="good in goods" :key="good.id">
          <td>{{ good.id }}</td>
          <td>{{ good.name }}</td>
          <td class="text-center">{{ good.quantity }}</td>
          <td class="text-right">{{ good.unitPrice }}</td>
          <td class="text-right">{{ good.amount }}</td>
        </tr>
          <tr>
            <td></td>
            <td></td>
            <td></td>
            <td class="sub-tb text-right">Subtotal</td>
            <td class="sub-tb text-right">{{ subTotal }}</td>
          </tr>
          <tr>
            <td></td>
            <td></td>
            <td></td>
            <td class="sub-tb text-right">VAT (7.5%)</td>
            <td class="sub-tb text-right">{{ VAT }}</td>
          </tr>
          <tr>
            <td></td>
            <td></td>
            <td></td>
            <th class="tot">TOTAL</th>
            <th class="tot text-right">{{ VAT + subTotal }}</th>
          </tr>
        </tbody>
      </table>

      <div class="fs-10 terms">
        <b>TERMS AND CONDITIONS</b>
        <p>
        Goods received in goods condition are not 
        </p>
      </div>

      <div class="fs-10 text-right">Signed by: <br/> <b>{{ businessDetails.name }}</b> <br/> Management</div>

      <div class="footer fs-10 text-center">Powered By <a href="https://payevi.vercel.app">PayEvi</a></div>

      <div class="bottom-line">
        <div class="hr-line"></div>
        <div class="hr-line"></div>
      </div>
    </div>
  </aside>
</template>

<script>
export default {
  name: "Table",
  data() {
    return {
      subTotal: "",
      VAT: "",
    }
  },
  props: {
    goods: Array,
    businessDetails: Object,
    clientDetails: Object,
    generated: Boolean,
  },
  methods: {
    getSubTotal() {
      if (!this.goods) {
        console.log("no goods found")
      } else {
        this.subTotal = 0;
        this.goods.filter(item => this.subTotal += item.amount)
      }
    },
    getVAT() {
      this.getSubTotal()
      let percent = 7.5 / 100
      this.VAT = this.subTotal * percent
    }
  },
  updated() {
        this.getSubTotal(),
        this.getVAT()
  },
};
</script>

<style scoped>
.tot {
  padding: 0 6px;
  font-size: 13px;
}
.sub-tb {
  font-weight: 600;
}
.bottom-line {
  padding: 0 30px;
  align-items: flex-end;
  display: flex;
  gap: 9px;
  background-color: rgb(10, 41, 28);
}

.hr-line {
  height: 18px;
  width: 12px;
  background-color: #fff;
}

aside {
  background-color: #fff;
  width: 105%;
  height: max-content;
  padding: 20px;
}

.footer {
  position: absolute;
  bottom: 20px;
  z-index: 10290;
  right: 3%;
  color: white;
  /* transform: translate(-50%, -50%); */
}

.fs-10 {
  font-size: 10px;
}

header {
  display: flex;
  padding: 0;
  align-items: center;
  justify-content: space-between;
}

.business-details {
    width: 200px;
    /* font-size: 13px; */
}

.business-details b, .business-details p {
  font-size: 9px;
  line-height: 9px;
}

h1 {
    font-size: 30px;
    font-weight: 600;
}

.container {
    padding: 20px 0;
}

.container .head {
    display: flex;
    align-items: flex-start;
    justify-content: space-between;
    padding: 18px 10px;
    font-size: 9px;
    line-height: 10px;
    background-color: rgb(178, 233, 210);
}

.client-details {
    width: 150px;
}

.client-details h3 {
  font-size: 11px;
}

.inv-row {
  display: flex;
  justify-content: space-between;
}

.invoice-details {
    width: 150px;
}

table {
  width: 100%;
  font-size: 9px;
}

tr {
  width: 100%;
  display: grid;
  /* font-size: 13px; */
  grid-template-columns: 30px 1fr 80px 70px 80px;
  gap: 10px;
}

th {
  background-color: var(--vt-c-black-mute);
  color: #fff;
}

td {
  padding: 6px 6px;
}

tbody {
  width: 100%;
  height: 400px;
}

.text-center {
  text-align: center;
}

.text-right {
  text-align: right;
}

td.remove {
  color: #ff0000;
  font-weight: 600;
  cursor: pointer;
}
</style>
