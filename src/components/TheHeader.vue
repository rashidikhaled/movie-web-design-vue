<template>
  <q-header class="bg-dark text-white" height-hint="64">
    <q-toolbar class="q-px-xl">
      <!-- Left Navbar Section -->
      <div class="row items-center q-gutter-x-sm">
        <q-btn
          flat
          round
          dense
          icon="account_circle"
          size="md"
          aria-label="Account" />
        <q-btn flat round dense icon="search" size="md" aria-label="Search" />
        <q-btn
          flat
          round
          dense
          icon="bookmark_border"
          size="md"
          aria-label="Bookmarks" />
        <q-btn
          flat
          round
          dense
          icon="notifications"
          size="md"
          aria-label="Notifications" />
        <q-btn
          flat
          round
          dense
          icon="arrow_back"
          size="md"
          aria-label="Go back"
          @click="$emit('back')" />
      </div>
      <!-- Right Navbar Section -->
      <div class="row items-center q-gutter-x-lg q-ml-auto">
        <div class="lt-md" v-if="isMobileMenuOpen">
          <q-btn
            flat
            round
            dense
            icon="close"
            @click="toggleMobileMenu"
            aria-label="Close menu" />
        </div>
        <div class="lt-md" v-else>
          <q-btn
            flat
            round
            dense
            icon="menu"
            @click="toggleMobileMenu"
            aria-label="Open menu" />
        </div>
        <div
          :class="[
            'row items-center q-gutter-x-lg',
            { hidden: isMobile && !isMobileMenuOpen },
          ]">
          <q-btn v-for="link in links" :key="link" flat dense :label="link" />
        </div>
        <img
          src="/logo.png"
          alt="Film Tarsnak Logo"
          class="q-ml-md logo"
          v-bind="$attrs" />
      </div>
    </q-toolbar>
  </q-header>
</template>

<script>
export default {
  name: "TheHeader",
  props: {
    links: {
      type: Array,
      default: () => [
        "دسته بندی ها",
        "فیلم",
        "سریال",
        "بازیگران",
        "جدیدترین دوبله",
      ],
    },
    logoUrl: {
      type: String,
      default: "https://via.placeholder.com/128x40",
    },
    logoAlt: {
      type: String,
      default: "Film Tarsnak Logo",
    },
  },
  data() {
    return {
      isMobileMenuOpen: false,
      isMobile: false,
    };
  },
  mounted() {
    this.checkScreenSize();
    window.addEventListener("resize", this.checkScreenSize);
  },
  beforeUnmount() {
    window.removeEventListener("resize", this.checkScreenSize);
  },
  methods: {
    toggleMobileMenu() {
      this.isMobileMenuOpen = !this.isMobileMenuOpen;
    },
    checkScreenSize() {
      this.isMobile = window.innerWidth < 768;
    },
  },
};
</script>

<style scoped>
.logo {
  width: 128.7px;
  height: 40px;
  object-fit: contain;
}

@media (max-width: 768px) {
  .hidden {
    display: none !important;
  }
}
</style>
