<template>
  <div class="main">
    <div class="loading"></div>
    <p>No Invoice generated yet</p>
  </div>
</template>

<style scoped>
.main {
  display: grid;
  place-items: center;
  color: var(--vt-c-text-dark-2);
  font-weight: 100;
  font-size: 12px;
  gap: 10px;
}
.loading {
  width: 30px;
  height: 30px;
  background-color: transparent;
  border: 3px solid var(--vt-c-text-dark-2);
  border-top: 3px solid transparent;
  border-radius: 50%;
  animation: rotate infinite linear 2s;
}

@keyframes rotate {
  0% {
    transform: rotate(0deg);
  }
  33% {
    transform: rotate(120deg);
  }
  66% {
    transform: rotate(240deg);
  }
  100% {
    transform: rotate(360deg);
  }
}
</style>
