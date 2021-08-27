<template>
  <q-layout view="lHh Lpr lFf">
    <q-header elevated>
      <q-toolbar>
        <q-btn
          flat
          dense
          round
          icon="menu"
          aria-label="Menu"
          @click="toggleLeftDrawer"
        />

        <q-toolbar-title> Quasar App </q-toolbar-title>

        <div>Quasar v{{ $q.version }}</div>
      </q-toolbar>
    </q-header>

    <q-footer class="bg-white" bordered>
      <q-tabs
        class="text-grey-10"
        active-color="primary"
        indicator-color="transparent"
      >
        <q-route-tab to="/" name="home" icon="eva-home-outline" label="Home" />
        <q-route-tab
          to="/camera"
          name="camera"
          icon="eva-camera-outline"
          label="Camera"
        />
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
