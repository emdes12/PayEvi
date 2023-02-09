<template>
  <aside id="print-invoice">
    <header>
      <div class="business-details">
        <h3>Emperor Designs</h3>
        <p>Graphics Designs, Web Development, Typist, Printing, and more</p>
        <p>+2349059084617</p>
      </div>
      <h1>INVOICE</h1>
    </header>

    <div class="container">
      <div class="head">
        <div class="client-details">
          <b>BILL TO:</b>
          <h4>Alawiye Muritala Adeshina</h4>
          <p>Apata, Agbowo-UI, Ibadan, Oyo State, Nigeria</p>
          <p>+2349024601558</p>
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
          <tr>
            <td>1.</td>
            <td>Red Velvet Cake 15inches high</td>
            <td class="text-center">2</td>
            <td class="text-right">1,200</td>
            <td class="text-right">2,400</td>
          </tr>
          <tr>
            <td>2.</td>
            <td>Classic Hamper boy Him (Valentine Pack)</td>
            <td class="text-center">1</td>
            <td class="text-right">60,000</td>
            <td class="text-right">60,000</td>
          </tr>
          <tr>
            <td>3.</td>
            <td>Red Velvet Cake 15inches high</td>
            <td class="text-center">2</td>
            <td class="text-right">1,200</td>
            <td class="text-right">2,400</td>
          </tr>
          <tr>
            <td></td>
            <td></td>
            <td></td>
            <th>TOTAL</th>
            <th>70,400</th>
          </tr>
        </tbody>
      </table>
    </div>
  </aside>
</template>

<script></script>

<style scoped>
aside {
  background-color: #fff;
  width: 8.5in;
  height: 11in;
  padding: 20px;
}

header {
  display: flex;
  padding: 0;
  align-items: center;
  justify-content: space-between;
}

.business-details {
    width: 300px;
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
    align-items: center;
    justify-content: space-between;
}

.client-details {
    width: 250px;
}

.invoice-details {
    width: 200px;
}

table {
  width: 100%;
}

tr {
  width: 100%;
  display: grid;
  font-size: 13px;
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
