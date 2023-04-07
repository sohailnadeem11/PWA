<template>
  <div id="app">
    <HeaderCheck :cartItemsCount="cartItemCount" @toggle-checkout="toggleCheckout" />
    <div class="container">
      <LessonList v-if="!showCheckout" @add-to-cart="addToCart" :products="products" />
      <LessonCheckout v-if="showCheckout" :cart="cart" @remove-from-cart="removeFromCart" @back-to-lessons="backToLessons" />
    </div>
  </div>
</template>

<script>
import LessonList from './components/NewLesson.vue';
import LessonCheckout from './components/LessonCheckout.vue';
import HeaderCheck from './components/Header.vue';
import { products } from './products.js';

export default {
  name: 'App',
  components: {
    LessonList,
    LessonCheckout,
    HeaderCheck,
  },
  data() {
    return {
      products: products,
      cart: [],
      showCheckout: false,
    };
  },
  computed: {
    cartItemCount() {
      let count = 0;
      for (const item of this.cart) {
        count += item.quantity;
      }
      return count;
    },
  },
  methods: {
    addToCart(productId) {
      const product = this.products.find((p) => p.id === productId);
      if (product.availableInventory > 0) {
        const cartItem = this.cart.find((item) => item.id === productId);
        if (cartItem) {
          cartItem.quantity++;
        } else {
          this.cart.push({ ...product, quantity: 1 });
        }
        product.availableInventory--;
      }
    },
    removeFromCart(productId) {
      const index = this.cart.findIndex((item) => item.id === productId);
      if (index !== -1) {
        const cartItem = this.cart[index];
        cartItem.quantity--;
        if (cartItem.quantity <= 0) {
          this.cart.splice(index, 1);
        }
        const product = this.products.find((p) => p.id === productId);
        product.availableInventory++;
      }
    },
    toggleCheckout() {
      this.showCheckout = !this.showCheckout;
    },
    backToLessons() {
      this.showCheckout = false;
    },
  },
};
</script>
