<template>
  <v-container>
    <SectionTitle title="Popular Movies" link="/movies/" />
    <v-row v-if="movies.length">
      <v-col cols="12" sm="4" v-for="movie in movies" :key="movie.id">
        <MovieCard :movie="movie" />
      </v-col>
    </v-row>
    <SectionTitle title="Upcoming Movies" link="/movies" />
    <v-row>
      <v-col cols="12" sm="4" v-for="u in upcoming" :key="u.id">
        <MovieCard :movie="u" />
      </v-col>
    </v-row>
    <SectionTitle title="Popular Casts" />
    <FeaturedCast :casts="featured_casts" />
  </v-container>
</template>
<script>
export default {
  layout: "homepage",
  data() {
    return {
      //
    };
  },
  head() {
    return {
      title: "Homepage",
    };
  },
  async asyncData({ $axios }) {
    try {
      const res = await $axios.$get("/movie/popular");
      const res2 = await $axios.$get("/movie/upcoming");
      const res3 = await $axios.$get("/person/popular");
      return {
        movies: res.results.slice(0, 6),
        upcoming: res2.results.slice(0, 6),
        featured_casts: res3.results.slice(0, 8),
      };
    } catch (e) {
      console.log(e);
    }
  },
};
</script>
