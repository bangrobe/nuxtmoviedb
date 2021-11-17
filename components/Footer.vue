<template>
  <v-footer dark padless>
    <v-card class="flex text-center" flat tile dense>
      <v-card-text class="grey darken-4">
        <strong class="subheading"
          >Get connected with us on social networks!</strong
        >

        <v-btn
          v-for="(item, i) in items"
          :key="i"
          dark
          icon
          :href="item.link"
          target="_blank"
        >
          <v-icon size="24px">
            {{ item.icon }}
          </v-icon>
        </v-btn>
      </v-card-text>

      <v-card-text class="py-2 white--text text-center">
        {{ new Date().getFullYear() }} — <strong>BangDigi</strong>
      </v-card-text>
    </v-card>
  </v-footer>
</template>
<script>
export default {
  name: "Footer",
  data() {
    return {
      items: [
        {
          icon: "mdi-youtube",
          link: "https://www.youtube.com/channel/UC7qEk915gA6SREYkvCsUW6A",
        },
        { icon: "mdi-earth", link: "https://bangdigi.com" },
      ],
    };
  },
};
</script>
