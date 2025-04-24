<template>
  <div class="column q-gutter-y-md movie-list">
    <div
      v-for="movie in movies"
      :key="movie.id"
      class="row items-center bg-grey-10 rounded-borders q-pa-xs movie-item"
      @click="$emit('select-movie', movie)">
      <!-- Poster -->
      <div class="relative-position movie-poster">
        <img
          :src="movie.poster"
          :alt="`${movie.title} Poster`"
          class="fit rounded-borders" />
        <q-btn
          round
          dense
          icon="play_circle"
          class="absolute-center bg-dark text-white play-btn" />
        <!-- Tags -->
        <div class="absolute-bottom-left row q-gutter-x-xs q-mb-xs q-ml-xs">
          <q-chip dense square color="green" text-color="white" icon="mic" />
          <q-chip
            dense
            square
            color="blue"
            text-color="white"
            icon="subtitles" />
          <q-chip
            dense
            square
            color="orange"
            text-color="white"
            icon="local_fire_department" />
        </div>
      </div>
      <!-- Info -->
      <div class="column q-pl-sm movie-info">
        <span class="text-subtitle1 text-weight-bolder">{{ movie.title }}</span>
        <span class="text-caption text-grey-7">{{ movie.genre }}</span>
        <span class="text-caption text-grey-7">{{ movie.year }}</span>
        <div class="row justify-between q-mt-xs">
          <div class="row items-center">
            <q-icon name="star" color="yellow" size="20px" />
            <span class="text-caption text-grey-7 q-ml-xs">{{
              movie.rating
            }}</span>
          </div>
          <span class="text-caption">{{ movie.duration }}</span>
        </div>
        <div class="row justify-between q-mt-xs q-pl-md ratings">
          <div class="row items-center">
            <q-icon
              name="analytics"
              color="primary"
              size="20px"
              class="q-mr-xs" />
            <span class="text-caption text-weight-bolder">{{
              movie.metacritic
            }}</span>
          </div>
          <div class="row items-center">
            <q-icon name="percent" color="red" size="20px" class="q-mr-xs" />
            <span class="text-caption text-weight-bolder">{{
              movie.rottenTomatoes
            }}</span>
          </div>
          <div class="row items-center">
            <q-icon name="star" color="amber" size="20px" class="q-mr-xs" />
            <span class="text-caption text-weight-bolder">{{
              movie.imdb
            }}</span>
          </div>
        </div>
      </div>
    </div>
    <q-btn
      flat
      dense
      icon="arrow_back"
      label="View More"
      class="bg-grey-10 text-white full-width"
      @click="$emit('view-more')" />
  </div>
</template>

<script>
export default {
  name: "MovieList",
  props: {
    movies: {
      type: Array,
      required: true,
    },
  },
};
</script>

<style scoped>
.movie-list {
  width: 384px;
}

.movie-poster {
  width: 88px;
  height: 122px;
}

.movie-info {
  width: 288px;
}

.play-btn {
  opacity: 0;
  transition: opacity 0.3s ease;
}

.movie-item:hover .play-btn {
  opacity: 0.8;
}

.ratings img {
  width: 20px;
  height: 20px;
  object-fit: contain;
}
</style>
