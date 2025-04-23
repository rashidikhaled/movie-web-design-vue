<template>
  <div class="row items-center q-mb-md">
    <q-btn
      flat
      dense
      icon="arrow_back"
      :label="label"
      class="bg-grey-10 text-white"
      @click="$emit('back')" />
  </div>
</template>

<script>
export default {
  name: "CtaSection",
  props: {
    label: {
      type: String,
      default: "Back",
    },
  },
};
</script>

<style scoped></style>
