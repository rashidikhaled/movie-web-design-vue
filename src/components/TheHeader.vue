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
      <div class="row items-center q-ml-auto">
        <!-- Mobile menu toggle button -->
        <div class="lt-md">
          <q-btn
            flat
            round
            dense
            :icon="isMobileMenuOpen ? 'close' : 'menu'"
            @click="toggleMobileMenu"
            aria-label="Toggle menu" />
        </div>

        <!-- Desktop navigation -->
        <div class="gt-sm row items-center q-gutter-x-lg my-font">
          <q-btn v-for="link in links" :key="link" flat dense :label="link" />
        </div>

        <!-- Logo -->
        <img
          :src="image"
          alt="Film Tarsnak Logo"
          class="q-ml-md logo"
          v-bind="$attrs" />
      </div>
    </q-toolbar>

    <!-- Mobile menu overlay -->
    <q-dialog
      v-model="isMobileMenuOpen"
      position="top"
      full-width
      transition-show="slide-down"
      transition-hide="slide-up"
      class="mobile-menu-dialog">
      <q-card class="bg-dark text-white">
        <q-card-section>
          <div class="column items-center q-gutter-y-md my-font">
            <q-btn
              v-for="link in links"
              :key="link"
              flat
              no-caps
              class="full-width text-center"
              size="lg"
              :label="link"
              @click="isMobileMenuOpen = false" />
          </div>
        </q-card-section>
      </q-card>
    </q-dialog>
  </q-header>
</template>

<script>
import image4 from "../assets/images/4.jpg";

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
      image: image4,
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

  .q-toolbar {
    padding-left: 8px !important;
    padding-right: 8px !important;
  }

  .q-gutter-x-sm {
    margin-left: -4px !important;
  }

  .q-gutter-x-sm > * {
    margin-left: 4px !important;
  }

  @media (max-width: 480px) {
    .logo {
      width: 100px;
      height: 32px;
    }

    .q-gutter-x-sm > * {
      margin-left: 2px !important;
    }

    .q-btn {
      padding: 4px !important;
      min-height: auto !important;
    }
  }
}

.mobile-menu-dialog .q-card {
  max-height: 80vh;
  overflow-y: auto;
}

.mobile-menu-dialog .q-btn {
  font-size: 18px;
  border-bottom: 1px solid rgba(255, 255, 255, 0.1);
  padding: 12px 0;
}

.my-font {
  font-family: "Yekan-Regular";
}
</style>
