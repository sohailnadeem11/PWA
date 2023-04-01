<template>
<main>
    <div v-for = "product in products" :key = "product.id">
        <h2>{{product.subject}}</h2>
        <figure>
            <img v-bind:src = "product.image" />
        </figure>
        <p v-html = "product.location"></p>
        <p>Price: {{ product.price }}</p>
        <p>Available Spaces: {{ product.availableInventory }}</p>
        <button @click="addToCart(product)"> Add to cart </button>
    </div>
</main>
</template>

<script>
export default {
    name: "ProductList",
    data() {
        return {
            products: [       
                {
                    id : 1001,
                    subject: 'Maths',
                    location: 'London',
                    price: 120,
                    image: "Maths.jpeg",
                    availableInventory: 5,
                    space: 5
                },
                {
                    id: 1002,
                    subject: 'English',
                    location: 'India',
                    price: 80,
                    image: "English.jpeg",
                    availableInventory: 5,
                    space: 5
                },
                {
                    id: 1003,
                    subject: 'Chemistry',
                    location: 'America',
                    price: 90,
                    image: "Chemistry.jpeg",
                    availableInventory: 5,
                    space: 5
                },
                {
                    id: 1004,
                    subject: 'Physics',
                    location: 'Mauritius',
                    price: 95,
                    image: "Physics.jpeg",
                    availableInventory: 5,
                    space: 5
                },
                {
                    id: 1005,
                    subject: 'Biology',
                    location: 'Dubai',
                    price: 110,
                    image: "Biology.jpeg",
                    availableInventory: 5,
                    space: 5                
                },
                { 
                    id: 1006,
                    subject: 'Geography',
                    location: 'Canada',
                    price: 100,
                    image: "Geography.jpeg",
                    availableInventory: 5,
                    space: 5
                },
                {
                    id: 1007,
                    subject: 'French',
                    location: 'London',
                    price: 80,
                    image: "French.jpeg",
                    availableInventory: 5,
                    space: 5
                },
                {
                    id: 1008,
                    subject: 'Spanish',
                    location: 'London',
                    price: 85,
                    image: "Spanish.jpeg",
                    availableInventory: 5,
                    space: 5
                },
                {
                   id: 1009,
                   subject: 'German',
                   location: 'Dubai',
                   price: 75,
                   image: "German.jpeg",
                   availableInventory: 5,
                   space: 5
                },
                {
                   id: 1010,
                   subject: 'Economics',
                   location: 'America',
                   price: 140,
                   image: "Economics.jpeg",
                   availableInventory: 5,
                   space: 5}
                ],
    methods: {
        add(product) {
         console.log("added product", product.id);
         this.$emit('addProduct',product);
        },
    },
    }},
};   
</script>
