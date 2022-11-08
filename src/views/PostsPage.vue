<template>
  <div>
    <h1>Post Page</h1>
    <MyInput v-model="searchQuery" placeholder="Search..." />
    <div class="app-btns">
      <MyButton @click="openPopup">Add post</MyButton>
      <MySelect v-model="selectedSort" :options="sortOptions" />
    </div>
    <MyPopup v-model:show="popupVisible">
      <PostForm @create="createPost" />
    </MyPopup>
    <PostList :posts="sortedAndSearchedPosts" @remove="remove" v-if="!isPostLoading" />
    <h2 style="text-align: center" v-else>Loading....</h2>
    <div class="page-wrapper">
      <div
        v-for="pageNumber in totalPages"
        :key="pageNumber"
        class="page"
        :class="{
          'current-page': page === pageNumber,
        }"
        @click="changePage(pageNumber)"
      >
        {{ pageNumber }}
      </div>
    </div>
  </div>
</template>

<script>
import PostForm from '@/components/PostForm.vue';
import PostList from '@/components/PostList.vue';
import MyButton from '@/components/UI/MyButton.vue';
import MyInput from '@/components/UI/MyInput.vue';
import axios from 'axios';
export default {
  components: {
    PostForm,
    PostList,
    MyButton,
    MyInput,
  },
  data() {
    return {
      posts: [],
      popupVisible: false,
      isPostLoading: false,
      selectedSort: '',
      searchQuery: '',
      page: 1,
      limit: 10,
      totalPages: 0,
      sortOptions: [
        { value: 'title', name: 'title' },
        { value: 'body', name: 'description' },
      ],
    };
  },
  methods: {
    createPost(newPost) {
      this.posts.push(newPost);
      this.popupVisible = false;
    },
    remove(post) {
      this.posts = this.posts.filter((item) => item !== post);
    },
    openPopup() {
      this.popupVisible = true;
    },
    changePage(pageNumber) {
      this.page = pageNumber;
    },
    async fetchPosts() {
      try {
        this.isPostLoading = true;
        const response = await axios.get('https://jsonplaceholder.typicode.com/posts', {
          params: {
            _page: this.page,
            _limit: this.limit,
          },
        });
        this.totalPages = Math.ceil(response.headers['x-total-count'] / this.limit);
        this.posts = response.data;
      } catch (e) {
        alert('Something went wrong');
      } finally {
        this.isPostLoading = false;
      }
    },
  },
  mounted() {
    this.fetchPosts();
  },
  computed: {
    sortedPosts() {
      return [...this.posts].sort((post1, post2) => {
        return post1[this.selectedSort]?.localeCompare(post2[this.selectedSort]);
      });
    },
    sortedAndSearchedPosts() {
      return this.sortedPosts.filter((post) =>
        post.title.toLowerCase().includes(this.searchQuery.toLowerCase()),
      );
    },
  },
  watch: {
    page() {
      this.fetchPosts();
    },
  },
};
</script>

<style>
.page-wrapper {
  margin: 15px 0;
  display: flex;
  justify-content: center;
}
.page {
  margin: 0 5px;
  padding: 5px;
  border: 1px solid #000;
  cursor: pointer;
}
.current-page {
  border: 2px solid teal;
}
</style>
