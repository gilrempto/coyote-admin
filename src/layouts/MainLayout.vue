<template>
  <q-layout view="lHh Lpr lFf">
    <w-header>
      <template v-slot:brand> Coyote Admin </template>
    </w-header>

    <w-sidebar :items="sidebarItems"></w-sidebar>

    <q-page-container>
      <router-view />
    </q-page-container>
  </q-layout>
</template>

<script>
import { defineComponent } from "vue";
import WHeader from "waves/components/WHeader.vue";
import WSidebar from "waves/components/WSidebar.vue";

const sidebarItems = [
  {
    icon: "las la-chart-bar",
    label: "Dashboard",
    link: "/",
  },
  {
    icon: "las la-boxes",
    label: "Products",
    link: "products",
  },
];

export default defineComponent({
  name: "MainLayout",

  components: {
    WHeader,
    WSidebar,
  },

  setup() {
    return {
      sidebarItems,
    };
  },
});
</script>
