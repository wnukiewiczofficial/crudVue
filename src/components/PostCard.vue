<template>
  <v-card
    class="text-left"
    color="indigo"
    variant="elevated"
    :title="title"
    :text="content"
  >
    <v-card-actions>
      <v-spacer />
      <v-btn @click="handleDelete(id)"> Delete </v-btn>
    </v-card-actions>
  </v-card>
</template>

<script>
import axios from "axios";
export default {
  name: "PostCard",
  props: {
    id: Number,
    title: String,
    content: String,
    deleteFunc: Function,
  },
  methods: {
    async deletePost(id) {
      // this.posts = this.posts.filter((user) => user.id !== id);
      try {
        const response = await axios.post(
          "http://localhost/api/crudVue/deletePost.php",
          {
            id,
          }
        );

        console.log(response.data);
        return true;
      } catch (error) {
        // console.error(error);
        return false;
      }
    },
    async handleDelete(id) {
      if (await this.deletePost(id)) {
        this.$emit("postDeleted");
      }
    },
  },
};
</script>
