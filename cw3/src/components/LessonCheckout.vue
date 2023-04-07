<style>
    #app{
            text-align: center;
            background-color: #EEEEEE;
            padding-bottom: 10px;
            padding-top: 10px;
            }
            img {
             border-radius: 40%;
            }
</style>
<template>
  <div>
    <h2>Checkout</h2>
    <div v-if="cart.length > 0">
      <ul>
        <li v-for="i in cart" :key="i.id" id="cart">
  <figure>
    <img :src="i.image" style="height: 80px" />
  </figure>
  <p>{{ i.subject }}</p>
  <p>{{ i.location }}</p>
  <p>{{ i.price }}</p>
  <button @click="removeFromCart(i.id)">Remove Subject</button>
</li>
      </ul>
      <form @submit.prevent="submitForm">
        <label for="name">Name:</label>
        <input type="text" id="name" v-model="name" :class="{ invalid: !nameIsValid }" required>
        <label for="phone">Phone Number:</label>
        <input type="text" id="phone" v-model="phone" :class="{ invalid: !phoneIsValid }" required>
        <button :disabled="!formIsValid">Checkout</button>
      </form>
      <button @click="backToLessons">Add More Lessons</button>
    </div>
    <div v-else>
      <p>No Lessons Added</p>
      <button @click="backToLessons">Home</button>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    cart: {
      type: Array,
      required: true,
    },
  },
  data() {
    return {
      name: '',
      phone: '',
      nameIsValid: false,
      phoneIsValid: false,
    };
  },
  computed: {
    formIsValid() {
      return this.nameIsValid && this.phoneIsValid;
    },
  },
  methods: {
    removeFromCart(productId) {
      this.$emit('remove-from-cart', productId);
    },
    backToLessons() {
      this.$emit('back-to-lessons');
    },
    submitForm() {
      if (!this.formIsValid) {
        alert('Please fill out all fields correctly');
        return;
      }

      // Clear the cart
      this.$emit('clear-cart');

      // Show thank you message
      alert('Order Submitted');

      // Reset the form fields
      this.name = '';
      this.phone = '';
      this.nameIsValid = false;
      this.phoneIsValid = false;
      location.reload();
      
    },
  },
  watch: {
    name() {
      this.nameIsValid = /^[a-zA-Z]+$/.test(this.name);
    },
    phone() {
        this.phoneIsValid = /^[0-9]{7,10}$/.test(this.phone);
      },
    },
  };
</script>

     
