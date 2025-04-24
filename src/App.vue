<template lang="">
  <q-layout view="lHh Lpr lFf">
    <!-- Navbar -->
    <the-header />
    <q-page-container>
      <q-page class="bg-dark q-pa-xl">
        <!-- CTA Section -->
        <cta-section @back="handleBack" />
        <!-- Tile Section -->
        <movie-tile
          :title="currentMovie.title"
          :rating="currentMovie.rating"
          :star-rating="3"
          @quality-changed="handleQualityChange" />
        <!-- Section 1: Movie List and Video -->
        <!-- Section 1: Movie List and Video -->
        <div class="row q-gutter-x-xl">
          <!-- Movie List -->
          <movie-list
            :movies="movies"
            @select-movie="selectMovie"
            @view-more="viewMoreMovies" />

          <!-- Video Player -->
          <video-player
            :thumbnail="currentMovie.thumbnail"
            :duration="150"
            @play="handlePlay"
            @seek="handleSeek" />
        </div>
      </q-page>
    </q-page-container>
  </q-layout>
</template>
<script>
import TheHeader from "./components/TheHeader.vue";
import CtaSection from "./components/CtaSection.vue";
import MovieTile from "./components/MovieTile.vue";
import MovieList from "./components/MovieList.vue";
import VideoPlayer from "./components/VideoPlayer.vue";

//images
import image1 from "./assets/images/1.jpg";
import image2 from "./assets/images/2.jpg";
import image3 from "./assets/images/3.jpg";

export default {
  name: "App",
  components: {
    TheHeader,
    CtaSection,
    MovieTile,
    MovieList,
    VideoPlayer,
  },
  data() {
    return {
      quality: "1080p",
      qualityOptions: ["1080p", "720p", "480p"],
      played: 0.3,
      currentMovieId: 1,
      movies: [
        {
          id: 1,
          title: "Movie One",
          genre: "Action, Adventure",
          year: "2023",
          rating: "8.5",
          duration: "2h 30m",
          metacritic: "75",
          rottenTomatoes: "80%",
          imdb: "8.5",
          poster: image1,
          thumbnail: image1,
        },
        {
          id: 2,
          title: "Movie Two",
          genre: "Drama, Romance",
          year: "2022",
          rating: "7.8",
          duration: "2h 15m",
          metacritic: "68",
          rottenTomatoes: "75%",
          imdb: "7.8",
          poster: image2,
          thumbnail: image2,
        },
        {
          id: 3,
          title: "Movie Three",
          genre: "Sci-Fi, Thriller",
          year: "2021",
          rating: "8.0",
          duration: "2h 45m",
          metacritic: "70",
          rottenTomatoes: "78%",
          imdb: "8.0",
          poster: image3,
          thumbnail: image3,
        },
      ],
    };
  },
  computed: {
    currentMovie() {
      return (
        this.movies.find((movie) => movie.id === this.currentMovieId) ||
        this.movies[0]
      );
    },
  },

  methods: {
    handleBack() {
      console.log("Back button clicked");
    },
    handleQualityChange(quality) {
      this.quality = quality;
      console.log("Quality changed to:", quality);
    },
    selectMovie(movie) {
      this.currentMovieId = movie.id;
      console.log("Movie selected:", movie.title);
    },
    viewMoreMovies() {
      console.log("View more movies clicked");
    },
    handlePlay(isPlaying) {
      console.log("Play state:", isPlaying ? "playing" : "paused");
    },
    handleSeek(event) {
      console.log("Seek to position:", event);
    },
  },
};
</script>
<style lang=""></style>
