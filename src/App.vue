<template>
  <header>
    <h1>Post CRUD Application</h1>
  </header>
  <main class="d-flex flex-column pa-6 ga-6" v-if="!isAdding">
    <v-btn variant="outlined" @click="() => (isAdding = true)">Add new</v-btn>
    <div :key="post.id" v-for="post in posts">
      <PostCard
        :id="post.id"
        :title="post.title"
        :content="post.content"
        :deleteFunc="deletePost"
        @postDeleted="getPosts"
      />
    </div>
  </main>
  <main class="d-flex flex-column pa-6 ga-6" v-if="isAdding">
    <PostAddForm
      :isAdding="isAdding"
      @postAdded="
        () => {
          isAdding = false;
          getPosts();
        }
      "
    />
  </main>
</template>

<script>
import axios from "axios";
import PostAddForm from "./components/PostAddForm.vue";
import PostCard from "./components/PostCard.vue";

export default {
  name: "App",
  components: { PostCard, PostAddForm },
  data() {
    return {
      // posts: [{ id: 0, title: "Title", content: "Content text" }],
      posts: [],
      isAdding: false,
    };
  },
  methods: {
    async getPosts() {
      try {
        const response = await axios.post(
          "http://localhost/api/crudVue/getPosts.php",
          {}
        );
        console.log(response.data);
        this.posts = response.data;
      } catch (error) {
        console.error(error);
      }
    },
  },
  mounted() {
    this.getPosts();
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
