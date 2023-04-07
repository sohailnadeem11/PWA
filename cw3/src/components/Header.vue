<template>
    <header>
      <div class="container">
        <h1>PWA</h1>
        <button v-if="cartItemsCount" @click="toggleCheckout">
          Shopping Cart {{ cartItemsCount }} 
          <span class="fa fa-shopping-cart"></span>
        </button>
        <!-- <button v-on:click='showCheckout' :disabled="checkoutVal">  
              {{cartItemsCount}} 
                <span class="fas fa-cart-plus"></span> Shopping Cart 
            </button> -->
      </div>
    </header>
  </template>
  
  <script>
export default {
  name: "HeaderCheck",
  props: {
    cartItemsCount: {
      type: Number,
      required: true,
    },
    isCheckoutVisible: {
      type: Boolean,
      required: true,
    },
  },
  methods: {
    toggleCheckout() {
      this.$emit("toggle-checkout");
    },
  },
};
  </script>