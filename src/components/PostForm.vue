<template>
  <form @submit.prevent>
    <h2>Create new post</h2>
    <MyInput v-model="post.title" class="input" type="text" placeholder="add title" />
    <MyInput v-model="post.body" class="input" type="text" placeholder="add description" />
    <MyButton class="btn-form" @click="createPost">add post</MyButton>
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
