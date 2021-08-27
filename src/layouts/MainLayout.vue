<template>
  <q-layout view="lHh Lpr lFf">
    <q-header class="bg-white text-grey-10" bordered>
      <q-toolbar>
        <q-btn
          to="/camera"
          flat
          round
          icon="eva-camera-outline"
          size="1.25rem"
          dense
          class="desktop-screen"
        />
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

    <q-footer class="bg-white mobile-screen" bordered>
      <q-tabs
        class="text-grey-10"
        active-color="primary"
        indicator-color="transparent"
      >
        <q-route-tab to="/" icon="eva-home-outline" label="Home" />
        <q-route-tab to="/camera" icon="eva-camera-outline" label="Camera" />
      </q-tabs>
    </q-footer>

    <q-page-container>
      <router-view />
    </q-page-container>
  </q-layout>
</template>

<script>
import { defineComponent, ref } from "vue";

export default {
  name: "MainLayout",

  data() {
    return {};
  },
};
</script>

<style lang="scss">
.q-header {
  .q-toolbar__title {
    font-size: 1.875rem;
    text-align: center;

    @media (min-width: $breakpoint-xs-max) {
      text-align: initial;
    }
  }
}

.q-footer {
  .q-tab__icon {
    font-size: 1.875rem;
  }
}
</style>
