<template>
  <v-row dense>
    <ProductBox
      v-for="product in latestProducts"
      v-bind:key="product._id"
      v-bind:product="product"
    />
  </v-row>
</template>

<script lang="ts">
import Vue from "vue";
// import HelloWorld from "../components/HelloWorld.vue";
import axios from "axios";
import ProductBox from "../components/ProductBox.vue";

export default Vue.extend({
  name: "Home",

  components: {
    ProductBox,
  },
  data: () => ({
    latestProducts: [],
  }),
  mounted() {
    this.getLatestProducts();
    document.title = "Home | My Online Store";
  },
  methods: {
    async getLatestProducts() {
      this.$store.commit("setIsLoading", true);
      await axios
        .get("/product")
        .then((response) => {
          this.latestProducts = response.data;
        })
        .catch((error) => {
          console.log(error);
        });
      this.$store.commit("setIsLoading", false);
    },
  },
});
</script>
