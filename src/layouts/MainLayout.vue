<template>
  <q-layout view="lHh Lpr lFf">
    <w-header>
      <template v-slot:brand>
        Coyote Admin
      </template>
    </w-header>

    <w-sidebar></w-sidebar>

    <q-page-container>
      <router-view />
    </q-page-container>
  </q-layout>
</template>

<script>
import { defineComponent } from "vue";
import WHeader from "waves/components/WHeader.vue";
import WSidebar from "waves/components/WSidebar.vue";

export default defineComponent({
  name: "MainLayout",

  components: {
    WHeader,
    WSidebar,
  },

  setup() {
    return {};
  },
});
</script>
