<template>
  <nav>
    <v-app-bar app color="primary darken-4" dense dark elevation="4">
      <v-app-bar-nav-icon
        @click="drawer = !drawer"
        v-if="auth"
      ></v-app-bar-nav-icon>

      <v-toolbar-title class="text-uppercase white--text">
        <!-- <span class="font-weight-light orange--text">My </span> -->
        <v-btn text to="/">My Online Store</v-btn>
        <!-- <span class="font-weight-bold green--text"> Store</span> -->
      </v-toolbar-title>

      <v-spacer></v-spacer>

      <v-btn text to="/cart">
        <v-icon left>shopping_cart-o</v-icon>
        <span>Cart ({{ cartTotalLength }})</span>
      </v-btn>

      <!-- <router-link to="/feed" tag="v-btn text">
        <v-btn color="black" flat value="auth">
          <span>Lofin</span>
        </v-btn>
      </router-link> -->

      <v-btn text to="/auth" v-if="!auth">
        <span>Sign In </span>
        <v-icon right>lock</v-icon>
      </v-btn>

      <v-btn text v-else>
        <span>Sign Out </span>
        <v-icon right>exit_to_app</v-icon>
      </v-btn>

      <!-- 
    <v-menu left bottom>
      <template v-slot:activator="{ on, attrs }">
        <v-btn text v-bind="attrs" v-on="on">
          Hi Username
        </v-btn>
      </template>

      <v-list>
        <v-list-item>
          <v-list-item-title>Profile</v-list-item-title>
        </v-list-item>
        <v-list-item>
          <v-list-item-title>Settings</v-list-item-title>
        </v-list-item>
        <v-list-item>
          <v-list-item-title>
            <v-icon right>exit_to_app</v-icon> SIGN OUT</v-list-item-title
          >
        </v-list-item>
      </v-list> 
    </v-menu>
    -->
    </v-app-bar>
    <v-navigation-drawer
      app
      v-model="drawer"
      class="primary darken-4"
      v-if="auth"
    >
      <p>Test</p>
    </v-navigation-drawer>
  </nav>
</template>

<script lang="ts">
import Vue from "vue";

export default Vue.extend({
  name: "Navbar",
  props: {
    cartTotalLength: Number,
  },

  data: () => ({
    drawer: true,
    auth: false,
  }),
  // computed: {
  //   cartTotalLength() {
  //     return this.$parent.cartTotalLength;
  //   },
  // },
});
</script>
