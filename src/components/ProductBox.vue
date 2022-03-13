<template>
  <v-col class="mb-4">
    <!-- <v-card>
      <v-img
        :src="card.src"
        class="white--text align-end"
        gradient="to bottom, rgba(0,0,0,.1), rgba(0,0,0,.5)"
        height="200px"
      >
        <v-card-title v-text="card.title"></v-card-title>
      </v-img>

      <v-card-actions>
        <v-spacer></v-spacer>

        <v-btn icon>
          <v-icon>mdi-heart</v-icon>
        </v-btn>

        <v-btn icon>
          <v-icon>mdi-bookmark</v-icon>
        </v-btn>

        <v-btn icon>
          <v-icon>mdi-share-variant</v-icon>
        </v-btn>
      </v-card-actions>
    </v-card> -->

    <v-card class="mx-auto" max-width="400">
      <v-img
        class="white--text align-end"
        height="200px"
        src="https://cdn.vuetifyjs.com/images/cards/docks.jpg"
      >
        <v-card-title>{{ product.name }}</v-card-title>
      </v-img>

      <v-card-subtitle class="pb-0 text--primary text--darken-4">
        ${{ product.price ? product.price : "12.9" }}
      </v-card-subtitle>

      <v-card-text>
        <div class="text--primary text--darken-4">Whitehaven Beach1</div>

        <div class="text--primary text--darken-4">
          Whitsunday Island, Whitsunday Islands
        </div>
      </v-card-text>

      <v-card-actions class="text-center">
        <v-btn color="primary darken-4" text @click="addToCart">
          Add To Cart
        </v-btn>

        <v-btn color="primary darken-4" text> Buy Now </v-btn>

        <v-btn color="primary darken-4" text> Details </v-btn>
      </v-card-actions>
    </v-card>

    <!-- <div class="box">
      <figure class="image mb-4">
        <img :src="product.get_thumbnail" />
      </figure>
      <h3 class="is-size-4">{{ product.name }}</h3>
      <p class="is-size-6 has-text-grey">${{ product.price }}</p>

      <router-link
        v-bind:to="product.get_absolute_url"
        class="button is-dark mt-4"
      >
        View Details
      </router-link>
    </div> -->
  </v-col>
</template>


<script lang="ts">
import Vue from "vue";

export default Vue.extend({
  name: "ProductBox",

  props: {
    product: Object,
  },

  data: () => ({
    //product: {},
    quantity: 1,
  }),
  mounted() {
    //this.getProduct();
  },
  methods: {
    // async getProduct() {
    //   this.$store.commit("setIsLoading", true);

    //   const category_slug = this.$route.params.category_slug;
    //   const product_slug = this.$route.params.product_slug;

    //   await axios
    //     .get(`/products/${category_slug}/${product_slug}/`)
    //     .then((response) => {
    //       this.product = response.data;

    //       document.title = this.product.name + " | My Online Store";
    //     })
    //     .catch((error) => {
    //       console.log(error);
    //     });
    //   this.$store.commit("setIsLoading", false);
    // },
    addToCart() {
      if (isNaN(this.quantity) || this.quantity < 1) {
        this.quantity = 1;
      }

      const item = {
        product: this.product,
        quantity: this.quantity,
      };

      this.$store.commit("addToCart", item);

      // toast({
      //   message: "The product was added to the cart.",
      //   type: "is-success",
      //   dismissible: true,
      //   pauseOnHover: true,
      //   duration: 2000,
      //   position: "bottom-right",
      // });
    },
  },
});
</script>
