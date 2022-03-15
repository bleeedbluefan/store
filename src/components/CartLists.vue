<template>
    <div class="wrapper">
        <div class="products">
            <div v-if="this.$root.$data.cart.length == 0">
                <p>EMPTY CART!</p>
            </div>
            <div v-else class="product" v-for="product in this.$root.$data.cart" :key="product.id">
                <div class="info">
                    <h1>{{product.product.name}} ({{product.quantity}})</h1>
                    <p>{{product.product.country}}</p>
                </div>
                <div class="image">
                    <img :src="'/images/products/'+product.product.image">
                </div>
                <div class="price">
                    <h2>{{product.product.price}}</h2>
                    <button class="auto" @click="itemSelected(product)">Remove</button>
                </div>
            </div>
        </div>
    </div>
</template>

<script>

// STANDARD EXPORT: 'name' is what it's called / 'props' is the data object transferred
export default {
    name: 'CartList',
    props: {
        products: Array
    },
    methods: {
        itemSelected(product) {
            let index = 0;
            for(let i = 0; i < this.$root.$data.cart.length; i++) {
                if (this.$root.$data.cart[i].product == product.product) {
                    index = i;
                    console.log("found product in cart");
                    if (this.$root.$data.cart[i].quantity > 1) {
                        console.log("it's too big");
                        this.$root.$data.cart[i].quantity -= 1;
                    }
                    else {
                        this.$root.$data.cart.splice(index, 1);  
                    }
                }
            }
            
            
        }
    }
}
</script>

<style scoped>
.wrapper {
    display: flex;
    align-items: center;
    justify-content: center;
}

.products {
    margin-top: 20px;
    display: flex;
    flex-wrap: wrap;
    justify-content: space-around;
}

.product {
    margin: 10px; 
    margin-top: 50px;
    width: 200px;
}

.product img {
    border: 2px solid #333;
    height: 250px;
    width: 200px;
    object-fit: cover;
}

.product .image {
    display: flex;
    justify-content: center;
    margin-bottom: 5px;
}

.info {
    background: #F2921D;
    color: #000;
    padding: 10px 30px;
    height: 80px;
}

.info h1 {
    font-size: 16px;
}

.info h2 {
    font-size: 14px;
}

.info p {
    margin: 0px;
    font-size: 10px;
}


.price {
    display: flex;
}

button {
    height: 50px;
    background: #000;
    color: white;
    border: none;
}

.auto {
    margin-left: auto;
}
</style>