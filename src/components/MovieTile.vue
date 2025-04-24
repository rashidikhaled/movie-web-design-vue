<template>
  <div class="row items-center justify-end q-mb-md">
    <q-btn flat round dense icon="search" class="bg-grey-10 q-mr-sm" />
    <q-btn flat round dense icon="share" class="bg-grey-10 q-mr-sm" />
    <q-btn flat round dense icon="view_module" class="bg-grey-10 q-mr-sm" />

    <!-- Ratings -->
    <div class="row items-center q-mr-sm">
      <img src="/imdb.png" alt="IMDB" class="q-mr-xs" />
      <span class="text-h6 text-weight-bolder">{{ rating }}</span>
      <span class="text-subtitle1 text-grey-7 q-ml-xs">/10</span>
    </div>

    <!-- Star Ratings -->
    <div class="row items-center q-mr-sm">
      <q-icon
        v-for="n in 5"
        :key="n"
        name="star"
        :color="n <= starRating ? 'yellow' : 'grey'"
        size="32px" />
    </div>

    <!-- Dropdown -->
    <q-select
      v-model="selectedQuality"
      :options="qualityOptions"
      standout
      bg-color="grey-10"
      color="white"
      class="q-mr-sm quality-select" />

    <!-- Movie Title and Resolution -->
    <div class="row items-center">
      <span class="text-h4 text-weight-bolder q-mr-md">{{ title }}</span>
      <div
        class="column items-center bg-red-10 text-white q-pa-xs rounded-borders">
        <span
          class="bg-grey-2 text-red-10 q-pa-xs rounded-borders text-caption text-weight-bolder">
          {{ quality }}
        </span>
        <span class="text-caption text-weight-bold">{{ format }}</span>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "MovieTile",
  props: {
    title: {
      type: String,
      default: "Movie Title",
    },
    rating: {
      type: String,
      default: "8.5",
    },
    starRating: {
      type: Number,
      default: 3,
    },
    quality: {
      type: String,
      default: "1080",
    },
    format: {
      type: String,
      default: "WebDL",
    },
    imdbLogo: {
      type: String,
      default: "https://via.placeholder.com/24x24",
    },
  },
  data() {
    return {
      selectedQuality: this.quality + "p",
      qualityOptions: ["1080p", "720p", "480p"],
    };
  },
  watch: {
    selectedQuality(val) {
      this.$emit("quality-changed", val);
    },
  },
};
</script>

<style scoped>
.quality-select {
  width: 183px;
}
</style>
