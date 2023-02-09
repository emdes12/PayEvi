<template>
  <form class="goods-form">
    <NotificationBar v-show="notifyShow" :notify="notify" />
    <h3>
      Goods <b v-if="goods.length">({{ goods.length }})</b>
    </h3>

    <table>
      <thead>
        <tr>
          <th>Description</th>
          <th>Quantity</th>
          <th>Unit Price</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="good in goods" :key="good.id">
          <Table :good="good" @remove-good="$emit('remove-good', good.id)" />
        </tr>
      </tbody>
    </table>

    <tr>
      <td>
        <input
          v-model="good.name"
          type="text"
          placeholder="goods description"
        />
      </td>
      <td>
        <input v-model="good.quantity" type="number" placeholder="quantity" />
      </td>
      <td>
        <input
          v-model="good.unitPrice"
          type="number"
          placeholder="unit price"
        />
      </td>
      <td @click="addToGoods" class="btn-add">+</td>
    </tr>

    <div class="btn-betw">
      <button @click="backToClient">Prev</button>
      <button @click="SubmitDetails">Generate Invoice</button>
    </div>
  </form>
</template>

<script>
import Table from "./Table.vue";
export default {
  name: "GoodsForm",
  data() {
    return {
      good: {
        name: "",
        unitPrice: "",
        quantity: "",
      },
      notifyShow: false,
      notify: {
        message: "",
        class: "",
      },
    };
  },
  components: {
    Table,
  },
  props: {
    goods: Array,
  },
  methods: {
    addToGoods() {
      if (!this.good.name) {
        this.$emit("no-fill");
      } else {
        const goodDetails = {
          id: this.goods.length + 1,
          name: this.good.name,
          quantity: this.good.quantity,
          unitPrice: this.good.unitPrice,
        };

        this.$emit("add-good", goodDetails);

        this.good.name = "";
        this.good.quantity = "";
        this.good.unitPrice = "";
      }
    },
    SubmitDetails(e) {
      e.preventDefault();
      this.$emit("generate-invoice");
    },
    backToClient(e) {
      e.preventDefault();
      this.$emit("to-client");
    },
  },
  emits: ["remove-good"],
};
</script>

<style scoped>
table {
  width: 100%;
}

tr {
  width: 100%;
  display: grid;
  grid-template-columns: 1fr 80px 90px 30px;
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
