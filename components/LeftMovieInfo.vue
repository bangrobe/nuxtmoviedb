<template>
  <v-banner sticky shaped tile>
    <v-img :src="`https://image.tmdb.org/t/p/w500${data.poster_path}`" />
    <v-card-text class="mt-4">
      <v-dialog v-model="dialog" persistent max-width="800px">
        <template v-slot:activator="{ on, attrs }">
          <v-btn
            color="pink"
            block
            depressed
            class="white--text"
            v-bind="attrs"
            v-on="on"
            @click.prevent="openYoutubeModal"
          >
            <v-icon>mdi-arrow-right-drop-circle-outline</v-icon> Watch trailer
          </v-btn>
        </template>
        <v-card>
          <v-card-title>
            <span class="headline"> {{ this.data.title }}</span>
          </v-card-title>
          <v-card-text>
            <v-container>
              <v-row>
                <v-col cols="12">
                  <div class="iframe-container">
                    <img :src="mediaUrl" v-if="!isVideo" />
                    <iframe
                      allowfullscreen
                      v-if="isVideo"
                      :src="mediaUrl"
                    ></iframe>
                  </div>
                </v-col>
              </v-row>
            </v-container>
          </v-card-text>
          <v-card-actions>
            <v-spacer> </v-spacer>
            <v-btn color="error" text @click="closeModal()">Close</v-btn>
          </v-card-actions>
        </v-card>
      </v-dialog>

      <v-btn
        v-if="data.homepage"
        color="yellow"
        block
        depressed
        :href="data.homepage"
        target="_blank"
        class="mt-2"
      >
        <v-icon>mdi-home</v-icon>Homepage
      </v-btn>
    </v-card-text>
  </v-banner>
</template>

<script>
export default {
  props: {
    data: {
      type: Object,
      required: true,
    },
  },
  data() {
    return {
      isVideo: false,
      mediaUrl: "",
      dialog: false,
    };
  },
  methods: {
    getTrailer() {
      if (!this.data.videos) return;
      // let trailers = [];
      // for (const item of this.data.videos.results) {
      //   if (item.type === "Trailer") {
      //     trailers.push(item.key);
      //   }
      // }
      //ES6 way
      const video = this.data.videos.results.find((e) => {
        return e.type === "Trailer";
      });
      return "https://www.youtube.com/embed/" + video.key;
    },
    openYoutubeModal() {
      this.mediaUrl = this.getTrailer();
      this.isVideo = true;
    },
    closeModal() {
      this.dialog = false;
      this.isVideo = false;
    },
  },
};
</script>

<style>
.iframe-container {
  overflow: hidden;
  padding-top: 56.25%;
  position: relative;
}

.iframe-container iframe {
  border: 0;
  height: 100%;
  left: 0;
  position: absolute;
  top: 0;
  width: 100%;
}
</style>
