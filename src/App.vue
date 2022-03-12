<template>
  <v-app>
    <navbar />
    <v-main>
      <v-container class="fill-height" fluid>
        <router-view v-slot="{ Component }">
          <transition
            enter-acitve-class="animate__animated animate__fadeInLeft"
            leave-acitve-class="animate__animated animate__fadeOutLeft"
            mode="out-in"
          >
            <component :is="Component" />
          </transition>
        </router-view>
      </v-container>
    </v-main>

    <v-footer app>
      <!-- -->
    </v-footer>
  </v-app>
</template>

<script lang="ts">
import Vue from "vue";
import Navbar from "./components/Navbar.vue";

export default Vue.extend({
  name: "App",

  components: {
    Navbar,
  },

  data: () => ({
    auth: true,
  }),
});
</script>
<style scoped>
.fade-enter-from,
.fade-leave-to {
  opacity: 0;
}

.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.5s ease-out;
}
</style>
