<script>
export default {
  name: "ClientForms",
  data() {
    return {
      client: {
        name: "",
        address: "",
        number: "",
      },
    };
  },
  methods: {
    moveToGoods(e) {
      e.preventDefault();
      if (!this.client.name) {
        this.$emit("no-fill");
      } else {
        const clientDetails = {
          name: this.client.name,
          address: this.client.address,
          number: this.client.number,
        };

        this.$emit("add-client", clientDetails);
      }
    },
    backToBusiness(e) {
      e.preventDefault();
      this.$emit("to-business");
    },
  },
};
</script>

<template>
  <form class="client-form">
    <h3>Customer's Details</h3>
    <div class="input-container">
      <label for="client-name">Client's Name:</label>
      <input
        type="text"
        v-model="client.name"
        id="client-name"
        placeholder="Customer's Name"
      />
    </div>

    <div class="input-container">
      <label for="client-address">Client's Address:</label>
      <input
        type="text"
        v-model="client.address"
        id="client-address"
        placeholder="Customer's Address"
      />
    </div>

    <div class="input-container">
      <label for="client-number">Client's Name:</label>
      <input
        type="number"
        v-model="client.number"
        id="client-number"
        placeholder="+2348012345678"
      />
    </div>

    <div class="btn-betw">
      <button @click="backToBusiness">Prev</button>
      <button @click="moveToGoods">Next</button>
    </div>
  </form>
</template>
