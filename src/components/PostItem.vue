<template>
  <div class="post">
    <div class="post-inner">
      <div><strong>Post:</strong> {{ post.id }}</div>
      <div><strong>Name:</strong> {{ post.title }}</div>
      <div><strong>Description:</strong> {{ post.body }}</div>
    </div>
    <div class="post-btns">
      <MyButton @click="$emit('remove', post)">Remove</MyButton>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    post: {
      type: Object,
      required: true,
    },
  },
};
</script>

<style scoped>
.post {
  margin-top: 15px;
  padding: 15px;
  border: 2px solid teal;
  display: flex;
  justify-content: space-between;
  align-items: center;
}
.post-inner {
  margin-right: 15px;
}
</style>
