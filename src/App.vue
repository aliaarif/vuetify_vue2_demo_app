<template>
  <v-app>
    <navbar v-bind:cartTotalLength="cartTotalLength" />
    <v-main>
      <v-container fluid>
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
import axios from "axios";

export default Vue.extend({
  name: "App",

  components: {
    Navbar,
  },

  data: () => ({
    showMobileMenu: false,
    cart: { items: [] },
  }),

  beforeCreate() {
    this.$store.commit("initializeStore");
    const token = this.$store.state.token;

    if (token) {
      axios.defaults.headers.common["Authorization"] = "Token " + token;
    } else {
      axios.defaults.headers.common["Authorization"] = "";
    }
  },
  mounted() {
    this.cart = this.$store.state.cart;
  },
  computed: {
    cartTotalLength(): number {
      let totalLength = 0;
      for (let i = 0; i < this.cart.items.length; i++) {
        totalLength += this.cart.items[i]["quantity"];
      }
      return totalLength;
    },
  },
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
