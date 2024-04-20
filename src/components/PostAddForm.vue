<template>
  <v-sheet class="mx-auto" size="small" width="300">
    <v-btn class="mr-auto" @click="() => $emit('postAdded')" color="#033"
      >Back</v-btn
    >
    <v-form fast-fail @submit.prevent @submit="handleSubmit" ref="form">
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
      <v-btn class="mt-2" type="submit" block>Add</v-btn>
    </v-form>
  </v-sheet>
</template>

<script>
import axios from "axios";

export default {
  name: "PostAddForm",
  data() {
    return {
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
    async addPost(title, content) {
      try {
        const response = await axios.post(
          "http://localhost/api/crudVue/addPost.php",
          {
            title,
            content,
          }
        );

        console.log(response.data);
        return true;
      } catch (error) {
        // console.error(error);
        return false;
      }
    },
    async handleSubmit() {
      const { valid } = await this.$refs.form.validate();
      if (valid) {
        const postAdded = await this.addPost(this.titleForm, this.contentForm);
        if (postAdded) this.$emit("postAdded");
      }
    },
  },
};
</script>
