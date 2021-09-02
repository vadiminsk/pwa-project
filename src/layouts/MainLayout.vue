<template>
  <q-layout view="lHh Lpr lFf">
    <q-header class="bg-white text-grey-10" bordered>
      <q-toolbar class="constrain">
        <q-btn
          to="/camera"
          flat
          round
          icon="eva-camera-outline"
          size="1.25rem"
          dense
          class="desktop-screen q-mr-xs"
        />
        <q-separator vertical spaced class="desktop-screen" />
        <q-toolbar-title class="text-grand-hotel text-bold">
          Quasargram
        </q-toolbar-title>
        <q-btn
          to="/"
          flat
          round
          icon="eva-home-outline"
          size="1.25rem"
          dense
          class="desktop-screen"
        />
      </q-toolbar>
    </q-header>

    <q-footer class="bg-white" bordered>
      <transition
        appear
        enter-active-class="animated fadeIn"
        leave-active-class="animated fadeOut"
      >
        <div v-if="showAppInstallBanner" class="banner-container bg-primary">
          <div class="constrain">
            <q-banner inline-actions dense class="bg-primary text-white">
              <template v-slot:avatar>
                <q-avatar
                  icon="eva-camera-outline"
                  color="white"
                  text-color="grey-10"
                  font-size="22px"
                />
              </template>
              <strong>Install app?</strong>

              <template v-slot:action>
                <q-btn
                  @click="installApp"
                  flat
                  dense
                  label="Yes"
                  class="q-px-sm"
                />
                <q-btn
                  @click="laterShowAppInstallBanner"
                  flat
                  dense
                  label="Later"
                  class="q-px-sm"
                />
                <q-btn
                  @click="neverShowAppInstallBanner"
                  flat
                  dense
                  label="Never"
                  class="q-px-sm"
                />
              </template>
            </q-banner>
          </div>
        </div>
      </transition>

      <q-tabs
        class="text-grey-10 mobile-screen"
        active-color="primary"
        indicator-color="transparent"
      >
        <q-route-tab to="/" icon="eva-home-outline" label="Home" />
        <q-route-tab to="/camera" icon="eva-camera-outline" label="Camera" />
      </q-tabs>
    </q-footer>

    <q-page-container class="bg-grey-1">
      <router-view />
    </q-page-container>
  </q-layout>
</template>

<script>
// Initialize deferredPrompt for use later to show browser install prompt.
let deferredPrompt;

export default {
  name: "MainLayout",

  data() {
    return {
      showAppInstallBanner: false,
    };
  },

  methods: {
    installApp() {
      // Hide the app provided install promotion
      this.showAppInstallBanner = false;
      // Show the install prompt
      deferredPrompt.prompt();
      // Wait for the user to respond to the prompt
      deferredPrompt.userChoice.then((choiceResult) => {
        if (choiceResult.outcome === "accepted") {
          console.log(`User accepted the install prompt`);
          this.neverShowAppInstallBanner();
        } else {
          console.log("User dismissed the install prompt");
        }
      });
    },

    laterShowAppInstallBanner() {
      this.showAppInstallBanner = false;
    },

    neverShowAppInstallBanner() {
      this.showAppInstallBanner = false;
      this.$q.localStorage.set("neverShowAppInstallBanner", true);
    },
  },

  mounted() {
    let neverShowAppInstallBanner = this.$q.localStorage.getItem(
      "neverShowAppInstallBanner"
    );

    if (!neverShowAppInstallBanner) {
      window.addEventListener("beforeinstallprompt", (e) => {
        // Prevent the mini-infobar from appearing on mobile
        e.preventDefault();
        // Stash the event so it can be triggered later.
        deferredPrompt = e;
        // Update UI notify the user they can install the PWA
        setTimeout(() => {
          this.showAppInstallBanner = true;
        }, 2000);
      });
    }
  },
};
</script>

<style lang="scss">
.q-header {
  .q-toolbar {
    @media (min-width: $breakpoint-xs-max) {
      height: 77px;
    }
    &__title {
      text-align: center;

      @media (min-width: $breakpoint-xs-max) {
        font-size: 1.875rem;
        text-align: initial;
      }
    }
  }
}

.q-footer {
  .q-tab__icon {
    font-size: 1.875rem;
  }
}
</style>
