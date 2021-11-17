<template>
  <v-sheet class="mx-auto">
    <v-slide-group multiple show-arrows>
      <v-slide-item v-for="cast in casts" :key="cast.id" v-slot="{ toggle }">
        <v-card @click="toggle" class="ma-4">
          <v-img
            cover
            width="240"
            height="280"
            :src="`https://image.tmdb.org/t/p/w500${cast.profile_path}`"
          />
        </v-card>
      </v-slide-item>
    </v-slide-group>
  </v-sheet>
</template>

<script>
export default {
  props: {
    casts: {
      type: Array,
      required: true,
    },
  },
};
</script>

<style></style>
