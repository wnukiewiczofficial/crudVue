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
      />
    </div>
  </main>
  <main class="d-flex flex-column pa-6 ga-6" v-if="isAdding">
    <v-sheet class="mx-auto" width="300">
      <v-form fast-fail @submit.prevent>
        <v-text-field
          :rules="generalRules"
          v-model="titleForm"
          label="Title"
        ></v-text-field>
        <v-text-field
          :rules="generalRules"
          v-model="contentForm"
          label="Content"
        ></v-text-field>
        <v-btn
          class="mt-2"
          block
          @click="
            () => {
              isAdding = false;
              addPost(titleForm, contentForm);
            }
          "
          >Add</v-btn
        >
      </v-form>
    </v-sheet>
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
      isAdding: false,
      titleForm: "",
      contentForm: "",
      generalRules: [
        (value) => {
          if (value != "") return true;
          return "Please input some text";
        },
      ],
    };
  },
  methods: {
    addPost(title, content) {
      this.posts.push({ id: this.posts.length, title, content });
    },
    deletePost(id) {
      this.posts = this.posts.filter((user) => user.id !== id);
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
