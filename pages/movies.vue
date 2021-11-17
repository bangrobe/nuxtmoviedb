<template>
  <v-container>
    <div class="text-center my-4">
      <v-btn value="popular" class="mr-2" @click="handleGetBy('popular')"
        >Popular</v-btn
      >
      <v-btn value="upcoming" class="mr-2" @click="handleGetBy('upcoming')"
        >Upcoming</v-btn
      >
      <v-btn value="top_rated" @click="handleGetBy('top_rated')"
        >Top Rated</v-btn
      >
    </div>
    <v-row v-if="$fetchState.pending">
      <v-col cols="12" sm="3" v-for="s in 20" :key="s">
        <v-skeleton-loader type="image, list-item-two-line"></v-skeleton-loader>
      </v-col>
    </v-row>
    <v-row v-else-if="$fetchState.error">
      <h2 class="error">An error occurred</h2>
    </v-row>
    <v-row v-else>
      <v-col cols="12" sm="3" v-for="movie in movies" :key="movie.id">
        <MovieCard :movie="movie" />
      </v-col>
    </v-row>
    <v-row>
      <v-col cols="12">
        <div class="text-center">
          <v-pagination
            v-model="currentPage"
            :total-visible="10"
            :length="totalPages"
            @input="handlePageChange"
          ></v-pagination>
        </div>
      </v-col>
    </v-row>
  </v-container>
</template>

<script>
export default {
  data() {
    return {
      movies: [],
      getBy: "popular",
      totalResults: 1,
      totalPages: 1,
      currentPage:
        parseInt(this.$route.query.page) > 1
          ? parseInt(this.$route.query.page)
          : 1,
    };
  },
  head() {
    return {
      title: "All movies",
    };
  },
  async fetch() {
    // console.log(query.name);
    await this.$axios
      .$get(`/movie/${this.getBy}?page=${this.currentPage}`)
      .then((res) => {
        this.totalResults = res.total_results;
        this.totalPages = res.total_pages;
        this.movies = res.results;
        this.$router.push({ query: { page: this.currentPage } });
      })
      .catch((e) => {
        console.log(e);
      });
  },
  methods: {
    handlePageChange(value) {
      this.currentPage = value;
      this.$fetch();
    },
    handleGetBy(value) {
      this.getBy = value;
      this.$fetch();
    },
  },
};
</script>

<style></style>
