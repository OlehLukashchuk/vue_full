<template>
  <button>
    <slot></slot>
  </button>
</template>

<script>
export default {
  name: 'my-button'
};
</script>

<style scoped>
button {
  background: none;
  border: 1px solid gray;
  border-radius: 5px;
  padding: 5px 10px;
  cursor: pointer;
}

button:active {
  transform: scale(0.9);
}
</style>