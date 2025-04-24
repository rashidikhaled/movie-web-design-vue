<template>
  <div class="row justify-end q-mt-md q-gutter-x-sm">
    <div
      class="row items-center bg-grey-10 rounded-borders q-pa-sm info-section">
      <q-btn
        flat
        dense
        label="Info"
        class="text-decoration-underline"
        @click="$emit('show-info')" />
      <span class="text-caption text-grey-7 q-ml-sm"
        >Additional Information</span
      >
      <q-icon name="info" color="grey-7" size="24px" />
    </div>
    <q-btn
      v-for="(player, index) in players"
      :key="index"
      flat
      dense
      :label="player.label"
      :class="player.class"
      :style="player.style"
      @click="$emit('select-player', player)" />
    <q-btn
      flat
      dense
      label="Download"
      class="bg-red-10 text-white download-btn"
      @click="$emit('download')" />
  </div>
</template>

<script>
export default {
  name: "PlayerOptions",
  data() {
    return {
      players: [
        {
          label: "Player 1",
          class: "bg-grey-10 text-white",
          style: "width: 140px",
        },
        {
          label: "Player 2",
          class: "bg-grey-10 text-white",
          style: "width: 140px",
        },
      ],
    };
  },
};
</script>

<style scoped>
.info-section {
  cursor: pointer;
  transition: background-color 0.3s ease;
}

.info-section:hover {
  background-color: #424242;
}

.download-btn {
  width: 158px;
}
</style>
