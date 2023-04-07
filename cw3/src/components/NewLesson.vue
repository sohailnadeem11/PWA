<template>
  <div class="lesson-list">
    <div class="search-bar">
      <input
        type="text"
        v-model="searchValue"
        placeholder="Search"
      />
            <select name="sortBy" id="select" v-model="sortBy">
                <option value="subject">Subject</option>
                <option value="location">Location</option>
                <option value="price">Price</option>
                <option value="space">Availability</option>
              </select>
              <button v-on:click="ascending = !ascending" class="sort-button">
                <i v-if="ascending" class="fa fa-sort-up"></i>
                <i v-else class="fa fa-sort-down"></i>
              </button>
    </div>
    <div v-for="product in sortedProducts" :key="product.id" class="lesson">
      <h3>{{ product.subject }}</h3>
      <figure>
        <img v-bind:src="product.image" style="height: 80px" />
      </figure>
      <p>{{ product.location }}</p>
      <p>Price: {{ product.price }}</p>
      <p v-if="product.availableInventory < 5">
        {{ product.availableInventory }} Spots left!!
      </p>
      <p v-else>Available Inventory: {{ product.availableInventory }}</p>
      <button
        @click="$emit('add-to-cart', product.id)"
        :disabled="product.availableInventory <= 0"
      >
        Add to cart
      </button>
    </div>
  </div>
</template>

<script>
export default {
  name: "LessonList",
  props: ["products"],
  data() {
    return {
      searchValue: "",
      sortField: "subject",
      sortOrder: "asc",
    };
  },
  computed: {
    sortedProducts() {
 let sortedProducts = this.products        

      sortedProducts = sortedProducts.sort((a, b) => {
            if (this.sortBy == 'subject') {
                let fa = a.subject.toLowerCase(), fb = b.subject.toLowerCase()

              if (fa < fb) {
                return -1
              }
              if (fa > fb) {
                return 1 
              }
              return 0
            }
            if (this.sortBy == 'location') {
                let fa = a.location.toLowerCase(), fb = b.location.toLowerCase()
              if (fa < fb) {
                return -1
              }
              if (fa > fb) {
                return 1 
              }
              return 0     
            }  
            if (this.sortBy == 'price') {
              return a.price - b.price
            }
            if (this.sortBy == 'space') {
              return a.space - b.space
            }
        }
        )
        if (!this.ascending) {
        	sortedProducts.reverse()
        }
      {
        const value= this.searchValue.charAt(0).toUpperCase() + this.searchValue.slice(1);
            return this.products.filter(function(product){
            return product.subject.indexOf(value) > -1 ||
                   product.location.indexOf(value) > -1
         })
        }

      return sortedProducts;
    },
  },
  methods: {
    updateSortedProducts() {
      this.sortedProducts; // this will trigger the computed property to recalculate
    },
  },
};
</script>
