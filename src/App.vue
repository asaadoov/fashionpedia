<template>
  <div id="app" class="container mt-5">
    <h1>Fashionpedia</h1>
    <NavBar 
      :cart="cart"
      :cartQty="cartQty"
      :cartTotal="cartTotal"
      @toggle="toggleSliderStatus"
      @deleteItem="deleteItem"
      ></NavBar>
    <price-slider :sliderStatus="sliderStatus" @upadteMaximum="upadteMaximum"></price-slider>
    <product-list :maximum="maximum" :products="products" @add="addItem"></product-list>
    
  </div>
</template>

<script>

// import { FontAwesomeIcon } from "@fortawesome/vue-fontawesome";
import ProductList from "./components/ProductList";
import PriceSlider from "./components/PriceSlider";
import NavBar from "./components/NavBar";

export default {
  name: "App",

  components: {
    ProductList,
    PriceSlider,
    NavBar
  },

  data: function() {
    return {
      maximum: 99,
      sliderStatus: true,
      cart:[],
      products: null
    }
  },

  computed: {
    cartTotal: function(){
			let sum= 0;
			this.cart.forEach(item => {
				sum += item.product.price * item.qty;
			});
			return sum;
		},
		cartQty: function(){
			let qty= 0;
			this.cart.forEach(item => {
				qty += item.qty;
			});
			return qty;
		},
  },

  methods: {
    upadteMaximum: function(maxAmount){
      this.maximum= maxAmount
    },
    toggleSliderStatus: function() {
      this.sliderStatus = !this.sliderStatus;
    },
    addItem: function(product){
			var productIndex ;
			var isExist = this.cart.filter((item, index) => {
				if(item.product.id == Number(product.id)){
					productIndex = index;
					return true;
				} else {
					return false;
				}
			});

			if(isExist.length){
				this.cart[productIndex].qty++;
			} else {
				this.cart.push( {product, qty: 1}	);
			}
    },
		deleteItem: function(id){
			
			if(this.cart[id].qty>1){
				this.cart[id].qty--;
			} else {
				this.cart.splice(id, 1);
			}
		}
    
  },

  mounted: function() {
		// fetch all the products when the component is mounted
		fetch('https://hplussport.com/api/products/order/price')
			.then(res => res.json())
      .then(data => this.products = data);
      console.log(this.products)
	}
  
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
