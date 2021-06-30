<template>
  <div class="wrapper">
    <div class="header">
      <h2 @click="goToShop()">Shop</h2>
      <div class="cart" @click="goToCart()">
          <img src="@/assets/img/icon-cart.svg" alt="cart" />
          <div id="counter2"><Counter /></div>
        </div>
    </div>

    <!-- SHOP  -->
    <div id="products" v-if="page === 'home'" class="">
      <h1>Products</h1>
      <div id="buttons">
        <input type="radio" id="radioAll" name="radioBtns" value="All" v-model="selectedCategory">
        <label for="radioAll">All</label>

        <input type="radio" id="radio2" name="radioBtns" value="Jacket" v-model="selectedCategory">
        <label for="radio2">Jackets</label>

        <input type="radio" id="radio3" name="radioBtns" value="Blazer" v-model="selectedCategory">
        <label for="radio3">Blazers</label> 

        <input type="radio" id="radio4" name="radioBtns" value="Tee" v-model="selectedCategory">
        <label for="radio4">Tees</label> 
      </div>
      <!-- PRODUCTS  -->
      <div id="product-loop" :key="product.id" v-for="product in filteredCategory">
        <product
          :isInCart="isInCart(product)"
          v-on:add-to-cart="addToCart(product)"
          :product="product"
        ></product>
      </div>
    </div> <!-- end "products" ie; Shop / 'home' -->
      
    <!-- CART  -->
    <div id="cart" v-if="page === 'cart'" class="">
      <h1>Cart</h1>
      <cart v-on:pay="pay()" v-on:remove-from-cart="removeFromCart($event)" :items="cart"></cart>
    </div>

    <!-- CHECKOUT  -->
    <div id="checkout" class="hidden">
      <h1>Checkout</h1>
      <Checkout />
    </div>

    <!-- ORDER CONFIRMATION  -->
    <div id="order-conf" class="hidden">
      <OrderConf />
    </div>

    <!-- pop-up, 'Shop' page  -->
    <div id="pop-up" class="opacity">
      <span class="close" @click="close()"><img src="../assets/img/close.svg" alt="close" /></span>
      <p><strong>Fur-neck Jacket </strong> has been added to your cart.</p>
    </div>

  </div> <!-- end "wrapper" -->
</template>

<script>
import products from "../data/products.json";
import Product from "./Product.vue";
import Cart from "./Cart.vue";
import Checkout from "./Checkout.vue";
import OrderConf from "./OrderConf.vue";
import Counter from './Counter.vue'

export default {
  components: {
    Product,
    Cart,
    Checkout,
    OrderConf,
    Counter
  },
  el:  "#product-loop",
  data () {
    return {
      products,
  		selectedCategory: "All",
      cart: [],
      page: 'home',
    }
  },
  props: ['value'], 
  methods: {
    goToShop() {
      this.page = 'home'
    },
    goToCart() {
      this.page = 'cart'
      document.getElementById('checkout').classList.add('hidden') 
      document.getElementById('order-conf').classList.add('hidden') 
      document.getElementById('cart').classList.remove('hidden') 
    },
    goToCheckout() {
      this.page = 'checkout';
    },

    addToCart(product) {
      this.cart.push(product);
      document.getElementById('pop-up').classList.remove('opacity')
      setTimeout(function() {
        document.getElementById('pop-up').classList.add('opacity')
      }, 2000);
    },
    isInCart(product) {
      const item = this.cart.find(item => item.id === product.id);
      if (item) {
        return true;
      }
      return false;
    },
    removeFromCart(product) {
      this.cart = this.cart.filter(item => item.id !== product.id);
    },
    pay() {
      this.cart = [];
      alert("Thanks! Shopping successfully completed. ");
    },
    close() {
      document.getElementById('pop-up').classList.add('hide')
    }
  },
	computed: {
		filteredCategory: function() {
			var vm = this;
			var category = vm.selectedCategory;
			
			if(category === "All") {
				return vm.products;
			} else {
				return vm.products.filter(function(product) {
					return product.category === category;
				});
			}
		}
	}

}

</script>

<style scoped>
.header h2:hover,
.cart:hover {
  cursor: pointer;
}

#checkout,
#order-conf {
  position: absolute;
  top: 50px;
  width: 100%;
}
.price {
    font-family: "XBold", sans-serif;
    font-weight: 900;
}
label {
    font-family: "Med", sans-serif;
}

input, button {
    border-radius: 10px;
    border: 2px #000 solid;
}
.header {
    display: flex;
    flex-direction: row;
    justify-content: space-between;
    padding: 10px 5%;
    border-bottom: 2px #000 solid;
}
h2 {font-size: 20px; margin: 0;}
.hide {display: none;}
.hidden {visibility: hidden;}
.opacity {
  opacity: 0;
  transition: ease-in-out 1s;
  z-index: 99999;
}

ul li {
  list-style: none;
}
#counter2 {
  border: 2px #000 solid;
  border-radius: 50%;
  background-color: #E9E7FC;
  width: 25px;
  height: 25px;
  position: absolute;
  top: 2px;
  right: 10px;
  font-family: "Bold", sans-serif;
  font-weight: 600;
  text-align: center;
  line-height: 160%;
}
.cart {
  margin-right: 10px;
}

/* pop-up box */
#pop-up {
  width: 83%;
  margin-left: 5%;
  padding: 2px 2px 2px 25px;
  border-radius: 15px;
  border: 2px #000 solid;
  box-shadow: 0 3px #000;
  background-color: #00C6AE;
  position: fixed;
  bottom: 20px;
  z-index: 99;
}
#pop-up p {
  font-family: "Bold", sans-serif; 
  font-size: 16px; 
  line-height: 150%;
  width: 80%;
  margin-top: 17px;
  }
#pop-up p strong {font-family: "XBold", sans-serif;}
#pop-up .close {
  width: 25px;
  height: 25px;
  background-color: #fff;
  border-radius: 50%;
  border: 2px #000 solid;
  box-shadow: 0 2px #000;
  text-align: center;
  line-height: 40%;
  float: right;
  cursor: pointer;
}
#pop-up .close img {
  width: 13px;
  height: auto;
  padding-top: 6px;
}


/* filter products radio-buttons */
#buttons {
  display: inline-block;
  padding-left: 4%;
}

#buttons input[type="radio"] {
  opacity: 0;
  position: fixed;
  width: 0;
}

#buttons label {
    display: inline-block;
    background-color: #fff;
    padding: 8px 15px;
    font-family: "XBold", sans-serif;
    font-size: 12px;
    border: 2px solid #000;
    border-radius: 30px;
    margin-right: 15px;
}

#buttons label:hover {
  background-color: #FFC7DE;
  cursor: pointer;
}

#buttons input[type="radio"]:checked + label {
    background-color: #FFC7DE;
}


</style>
