<template lang="">
  <q-layout view="lHh Lpr lFf">
    <!-- Navbar -->
    <the-header />
    <q-page-container>
      <q-page class="bg-dark q-pa-xl">
        <!-- CTA Section -->
        <cta-section @back="handleBack" />
      </q-page>
    </q-page-container>
  </q-layout>
</template>
<script>
import TheHeader from "./components/TheHeader.vue";
import CtaSection from "./components/CtaSection.vue";

export default {
  name: "App",
  components: {
    TheHeader,
    CtaSection,
  },
  methods: {
    handleBack() {
      console.log("Back button clicked");
    },
  },
};
</script>
<style lang=""></style>
