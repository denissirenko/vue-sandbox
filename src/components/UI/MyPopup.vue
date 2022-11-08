<template>
  <div class="popup" v-if="show" @click="hideDialog">
    <div class="popup-content" @click.stop>
      <slot></slot>
    </div>
  </div>
</template>

<script>
export default {
  name: 'MyPopup',
  props: {
    show: {
      type: Boolean,
      default: false,
    },
  },
  methods: {
    hideDialog() {
      this.$emit('update:show', false);
    },
  },
};
</script>

<style scoped>
.popup {
  display: flex;
  position: fixed;
  top: 0;
  right: 0;
  bottom: 0;
  left: 0;
  background-color: rgba(0, 0, 0, 0.5);
}
.popup-content {
  padding: 30px 50px;
  margin: auto;
  background-color: white;
  border-radius: 8px;
  min-width: 500px;
}
</style>
