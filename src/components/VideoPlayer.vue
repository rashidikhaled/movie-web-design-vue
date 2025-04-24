<template>
  <div class="relative-position video-player">
    <img :src="thumbnail" alt="Video Thumbnail" class="fit rounded-borders" />
    <!-- Video Controls -->
    <div class="absolute-bottom full-width bg-dark video-controls">
      <div class="row items-center justify-between q-px-sm">
        <!-- Left Controls -->
        <div class="row items-center">
          <q-btn flat round dense icon="play_arrow" @click="togglePlay" />
          <q-btn flat round dense icon="skip_next" @click="skipForward" />
          <q-btn flat round dense icon="volume_up" @click="toggleMute" />
          <span class="text-caption"
            >{{ formatTime(currentTime) }} / {{ formatTime(duration) }}</span
          >
        </div>
        <!-- Right Controls -->
        <div class="row items-center">
          <q-btn flat round dense icon="high_quality" @click="toggleQuality" />
          <q-btn
            flat
            round
            dense
            icon="picture_in_picture"
            @click="togglePip" />
          <q-btn flat round dense icon="fullscreen" @click="toggleFullscreen" />
        </div>
      </div>
      <!-- Progress Bar -->
      <q-linear-progress
        :value="progress"
        color="red"
        track-color="grey-5"
        class="absolute-bottom progress-bar"
        @click="seek" />
    </div>
  </div>
</template>

<script>
export default {
  name: "VideoPlayer",
  props: {
    thumbnail: {
      type: String,
      default: "https://via.placeholder.com/792x456",
    },
    duration: {
      type: Number,
      default: 150, // in seconds
    },
  },
  data() {
    return {
      isPlaying: false,
      isMuted: false,
      isFullscreen: false,
      isPip: false,
      showQualityMenu: false,
      currentTime: 0,
      progress: 0.3, // between 0 and 1
    };
  },
  methods: {
    togglePlay() {
      this.isPlaying = !this.isPlaying;
      this.$emit("play", this.isPlaying);
    },
    toggleMute() {
      this.isMuted = !this.isMuted;
      this.$emit("mute", this.isMuted);
    },
    toggleFullscreen() {
      this.isFullscreen = !this.isFullscreen;
      this.$emit("fullscreen", this.isFullscreen);
    },
    togglePip() {
      this.isPip = !this.isPip;
      this.$emit("pip", this.isPip);
    },
    toggleQuality() {
      this.showQualityMenu = !this.showQualityMenu;
      this.$emit("quality-menu", this.showQualityMenu);
    },
    skipForward() {
      this.currentTime += 10;
      if (this.currentTime > this.duration) {
        this.currentTime = this.duration;
      }
      this.updateProgress();
      this.$emit("skip");
    },
    updateProgress() {
      this.progress = this.currentTime / this.duration;
    },
    seek(event) {
      // Calculate seek position based on click position
      this.$emit("seek", event);
    },
    formatTime(seconds) {
      const minutes = Math.floor(seconds / 60);
      const remainingSeconds = Math.floor(seconds % 60);
      return `${minutes.toString().padStart(2, "0")}:${remainingSeconds
        .toString()
        .padStart(2, "0")}`;
    },
  },
};
</script>

<style scoped>
.video-player {
  width: 792px;
  height: 456px;
}

.video-controls {
  height: 36px;
}

.progress-bar {
  height: 3px;
  cursor: pointer;
}
</style>
