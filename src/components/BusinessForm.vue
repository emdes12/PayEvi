<template>
  <form class="business-form" @submit="moveToClient">
    <h3>Your Business Details</h3>
    <div class="input-container">
      <label for="name">Business Name:</label>
      <input
        type="text"
        id="name"
        v-model="business.name"
        placeholder="Your Business Name"
      />
    </div>

    <div class="input-container">
      <label for="description">Business Description:</label>
      <input
        type="text"
        id="description"
        v-model="business.description"
        placeholder="What you do"
      />
    </div>

    <div class="input-container">
      <label for="business-phone">Your Contact:</label>
      <input
        type="number"
        id="business-phone"
        v-model="business.number"
        placeholder="+2348012345678"
      />
    </div>

    <div class="btn-right">
      <button>Next</button>
    </div>
  </form>
</template>

<script>
export default {
  name: "BusinessForm",
  data() {
    return {
      business: {
        name: "",
        description: "",
        number: "",
      },
    };
  },
  methods: {
    moveToClient(e) {
      e.preventDefault();
      if (!this.business.name) {
        this.$emit("no-fill");
      } else {
        const businessDetails = {
          name: this.business.name,
          description: this.business.description,
          number: this.business.number,
        };

        this.$emit("add-business", businessDetails);
      }
    },
  },
};
</script>
