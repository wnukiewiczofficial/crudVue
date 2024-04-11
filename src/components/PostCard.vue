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
      <v-btn @click="deleteFunc(id)"> Delete </v-btn>
    </v-card-actions>
  </v-card>
</template>

<script>
export default {
  name: "PostCard",
  props: {
    id: Number,
    title: String,
    content: String,
    deleteFunc: Function,
  },
};
</script>
