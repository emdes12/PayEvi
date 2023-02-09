<template>
  <div :class="notify.class">
    <h3>{{ notify.message }}</h3>
  </div>
</template>

<script>
export default {
  props: {
    notify: Object,
  },
};
</script>

<style scoped>
.notification-bar {
  max-width: 450px;
  padding: 8px 12px;
  width: fit-content;
  position: absolute;
  top: 50px;
  left: 50%;
  transform: translate(-50%, -50%);
  transition: display ease-in-out 3s;
  background-color: hsla(160, 100%, 37%, 1);
}

.error {
  background-color: #ff0000;
}

h3 {
  color: #fff;
  font-size: 12px;
}
</style>
