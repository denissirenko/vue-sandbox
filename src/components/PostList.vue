<template>
  <div v-if="posts.length > 0">
    <h2 style="text-align: center">Posts</h2>
    <TransitionGroup name="post-list">
      <PostItem v-for="post in posts" :post="post" :key="post.id" @remove="$emit('remove', post)" />
    </TransitionGroup>
  </div>
  <h1 v-else>Post list is empty</h1>
</template>

<script>
import { TransitionGroup } from 'vue';
import PostItem from './PostItem.vue';
export default {
  components: {
    PostItem,
    TransitionGroup,
  },
  props: {
    posts: {
      type: Array,
    },
  },
};
</script>

<style scoped>
.post-list-move,
.post-list-enter-active,
.post-list-leave-active {
  transition: all 0.5s ease;
}

.post-list-enter-from,
.post-list-leave-to {
  opacity: 0;
  transform: translateX(30px);
}
.post-list-leave-active {
  position: absolute;
}
</style>
