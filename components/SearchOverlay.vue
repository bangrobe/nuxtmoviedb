<template>
  <v-overlay :value="overlay" dark opacity="0.95">
    <Search />
    <v-btn v-if="overlay" @click="overlay = false">Close</v-btn>
  </v-overlay>
</template>

<script>
export default {
  data: () => ({
    overlay: false,
  }),
  created() {
    this.$nuxt.$on("openOverload", ($event) => this.handleOverload($event));
  },
  methods: {
    handleOverload(e) {
      this.overlay = e;
    },
  },
  watch: {
    $route(to, from) {
      this.overlay = false;
    },
  },
};
</script>

<style></style>
