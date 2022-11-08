<template>
  <div class="app">
    <RouterView></RouterView>
  </div>
</template>

<script>
export default {};
</script>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}
.app {
  margin: 0 auto;
  max-width: 1200px;
  padding: 0 15px;
}
.app-btns {
  margin: 15px 0;
  display: flex;
  justify-content: space-between;
}
h1 {
  text-align: center;
}
</style>
