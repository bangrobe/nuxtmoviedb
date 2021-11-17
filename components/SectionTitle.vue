<template>
  <v-toolbar class="my-4" outlined short flat>
    <v-toolbar-title>{{ title }}</v-toolbar-title>
    <v-spacer></v-spacer>

    <v-btn text :to="link" color="pink"
      >See more <v-icon right>mdi-chevron-double-right</v-icon></v-btn
    >
  </v-toolbar>
</template>

<script>
export default {
  props: {
    title: {
      type: String,
      required: true,
    },
    link: {
      type: String,
      required: false,
    },
  },
};
</script>

<style></style>
