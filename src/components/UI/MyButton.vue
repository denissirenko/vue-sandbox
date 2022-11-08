<template>
  <button class="btn">
    <slot></slot>
  </button>
</template>

<script>
export default {
  name: 'MyButton',
};
</script>

<style scoped>
.btn {
  padding: 5px 15px;
  cursor: pointer;
  color: white;
  background-color: teal;
  border: 1px solid teal;
}
.btn:disabled {
  opacity: 0.7;
  cursor: auto;
}
</style>
