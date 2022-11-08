<template>
  <form @submit.prevent>
    <h3>Create new post</h3>
    <MyInput v-model="post.title" class="input" type="text" placeholder="add title" />
    <MyInput v-model="post.body" class="input" type="text" placeholder="add description" />
    <MyButton
      :disabled="post.title.length === 0 || post.body.length === 0"
      class="btn-form"
      @click="createPost"
      >add post</MyButton
    >
  </form>
</template>

<script>
export default {
  data() {
    return {
      post: {
        title: '',
        body: '',
      },
    };
  },
  methods: {
    createPost() {
      this.post.id = Date.now();
      this.$emit('create', this.post);
      this.post = {
        title: '',
        body: '',
      };
    },
  },
};
</script>

<style scoped>
form {
  display: flex;
  flex-direction: column;
}
.btn-form {
  align-self: flex-end;
  margin-top: 15px;
}
</style>
