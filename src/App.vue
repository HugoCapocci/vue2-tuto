<template>
  <div id="app">

    <div class="product">

      <div class="product-image">
        <img :src="image" :alt="altText" />
      </div>

      <div class="product-info">
        <h1>{{ product }}</h1>
        <p v-if="inventory >= 10">In Stock</p>
        <p v-else-if="inventory > 0 && inventory < 10">Almost sold out...</p>
        <p v-else>Out of Stock!</p>
        <ul>
          <li v-for="(detail, index) in details" :key="index">
            {{ detail }}
          </li>
        </ul>
        <div v-for="variant in variants" :key="variant.variantId">
          <p @mouseover="changeColor(variant.variantColor)">{{ variant.variantColor }}</p>
        </div>

        <div class="spaced">
          <button @click="addToCart">Add to cart</button>
          <button @click="removeFromCart" :disabled="cart <= 0">Remove from cart</button>
        </div>

        <div class="cart">
          <p>Cart({{ cart }})</p>
        </div>
      </div>

    </div>
  </div>
</template>

<script>

export default {
  name: 'app',
  data() {
    return {
      product: 'Socks',
      inventory: 50,
      models: {
        green: 'https://dl.dropboxusercontent.com/s/9zccs3f0pimj0wj/vmSocks-green-onWhite.jpg?dl=0',
        blue: 'https://www.dropbox.com/s/t32hpz32y7snfna/vmSocks-blue-onWhite.jpg?dl=0'
      },
      image: 'https://dl.dropboxusercontent.com/s/9zccs3f0pimj0wj/vmSocks-green-onWhite.jpg?dl=0',
      altText: 'A pair of stocks',
      details: ['80% cotton', '20% polyester', 'Gender-neutral'],
      variants: [
        {
          variantId: 2234,
          variantColor: 'green'    
        },
        {
          variantId: 2235,
          variantColor: 'blue'
        }
      ],
      cart: 0,
    };
  },
  methods: {
    addToCart() {
      this.cart += 1;
    },
    removeFromCart() {
      this.cart -= 1
    },
    changeColor(color) {
      console.log('color changed: ', color);
      this.image = this.models[color];
    },
  }
}
</script>

<style>
body {
  font-family: tahoma;
  color: #282828;
  margin: 0px;
}

.nav-bar {
  background: linear-gradient(-90deg, #84CF6A, #16C0B0);
  height: 60px;
  margin-bottom: 15px;
}

.product {
  display: flex;
}

img {
  border: 1px solid #d8d8d8;
  width: 70%;
  margin: 40px;
  box-shadow: 0px .5px 1px #d8d8d8;
}

.product-image {
  flex-basis: 700px;
}

.spaced {
  display: flex;
}
.spaced > button{
  margin-right: 2px;
}

.product-info {
  margin-top: 10px;
  flex-basis: 500px;
}

.color-box {
  width: 40px;
  height: 40px;
  margin-top: 5px;
}

.cart {
  margin-right: 25px;
  float: right;
  border: 1px solid #d8d8d8;
  padding: 5px 20px;
}

button {
  margin-top: 30px;
  border: none;
  background-color: #1E95EA;
  color: white;
  height: 40px;
  width: 100px;
  font-size: 14px;
} 

.disabledButton {
  background-color: #d8d8d8;
}

.review-form {
  width: 30%;
  padding: 20px;
  border: 1px solid #d8d8d8;  
}

input {
  width: 100%;  
  height: 25px;
  margin-bottom: 20px;
}

textarea {
  width: 100%;
  height: 60px;
}
</style>
