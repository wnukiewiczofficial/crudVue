<template>
  <header>
    <h1>Post CRUD Application</h1>
  </header>
  <main class="d-flex flex-column pa-6 ga-3">
    <div :key="post.id" v-for="post in posts">
      <PostCard :title="post.title" :content="post.content" />
    </div>
  </main>
</template>

<script>
import PostCard from "./components/PostCard.vue";
export default {
  name: "App",
  components: { PostCard },
  data() {
    return {
      posts: [{ id: 0, title: "Title", content: "Content text" }],
    };
  },
  methods: {
    addPost(title, content) {
      this.posts.push({ id: this.posts.length, title, content });
    },
    deletePost() {
      // Here deleting
    },
  },
  mounted() {
    this.addPost("Siema", "Pedaly");
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
