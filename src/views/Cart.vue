<template>
  <div class="page-cart">
    <div class="columns is-multiline">
      <div class="column is-12">
        <h1 class="title">Cart</h1>
      </div>

      <div class="column is-12 box">
        <table class="table is-fullwidth" v-if="cartTotalLength">
          <thead>
            <th>Product</th>
            <th>Price</th>
            <th>Quantity</th>
            <th>Total</th>
            <th></th>
          </thead>
          <tbody>
            <CartItem
              v-for="item in cart.items"
              v-bind:key="item.product.id"
              v-bind:initialItem="item"
              v-on:removeFromCart="removeFromCart"
            />
          </tbody>
        </table>
        <p v-else>You dont have any product in your cart...</p>
      </div>

      <div class="column is-12 box" v-if="cartTotalLength">
        <h2 class="subtitle">Summary</h2>
        <strong>${{ cartTotalPrice.toFixed(2) }}</strong
        >, {{ cartTotalLength }} items
        <hr />
        <router-link to="/cart/checkout" class="button is-dark">
          Proceed to Checkout
        </router-link>
      </div>
      <div class="column is-12 box" v-else>
        <router-link to="/" class="button is-dark">
          Continue Shopping
        </router-link>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";
// import { toast } from "bulma-toast";
import CartItem from "@/components/CartItem.vue";

export default {
  name: "Cart",
  components: {
    CartItem,
  },
  data() {
    return {
      cart: {
        items: [],
      },
    };
  },
  mounted() {
    this.$store.commit("setIsLoading", true);
    this.cart = this.$store.state.cart;
    document.title = "Cart | My Online Store";
    this.$store.commit("setIsLoading", false);
  },
  computed: {
    cartTotalLength() {
      return this.cart.items.reduce((acc, curVal) => {
        return (acc += curVal.quantity);
      }, 0);
    },
    cartTotalPrice() {
      return this.cart.items.reduce((acc, curVal) => {
        return (acc += curVal.product.price * curVal.quantity);
      }, 0);
    },
  },
  methods: {
    removeFromCart(item) {
      this.cart.items = this.cart.items.filter(
        (i) => i.product.id !== item.product.id
      );
    },
  },
};
</script>
