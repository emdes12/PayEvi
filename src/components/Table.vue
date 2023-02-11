<template>
  <td>{{ good.name }}</td>
  <td class="text-center">{{ good.quantity }}</td>
  <td class="text-right">{{ good.unitPrice }}</td>
  <td class="remove" @click="onRemove(good.id)">x</td>
</template>

<script>
export default {
  name: "Table",
  props: {
    good: Object,
  },
  methods: {
    onRemove(id) {
      this.$emit("remove-good", id);
    },
  },
  emits: ["remove-good"],
};
</script>

<style scoped>
td {
  color: #fff;
  padding: 0 13px;
}

td.remove {
  color: #ff0000;
}
</style>
