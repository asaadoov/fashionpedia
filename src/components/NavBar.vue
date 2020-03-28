<template>
	<nav 
			class="navbar navbar-light fixed-top mb-3" >

			<div class="navbar-text ml-auto d-flex">
				<button 
					class="btn btn-sm btn-outline-success" @click="$emit('toggle')">
						<font-awesome-icon icon="dollar-sign"></font-awesome-icon>
				</button>
				<!-- v-if="cart.length>0" -->
				<div class="dropdown ml-2" v-if="cart.length>0">
					<button class="btn btn-success btn-sm dropdown-toggle" 
						id="cartDropdown" data-toggle="dropdown" 
						aria-haspopup="true" aria-expanded="false">

						<!-- <b>cart:</b>  -->
						<span class="badge badge-pill badge-light">{{ cartQty}}</span>
						<font-awesome-icon icon="shopping-cart" class="mr-2"></font-awesome-icon>
						<price :value="Number(cartTotal)"></price>
					</button>
					<div class="dropdown-menu dropdown-menu-right" aria-labelledby="cartDropdown">
						<div v-for="(item, index) in cart" :key="index">
							<div class="dropdown-item-text text-nowrap text-right">
								<span class="badge badge-pill badge-warning align-text-top nr-1">{{ item.qty }}</span>
								{{ item.product.name }}
								<b><price :value="Number(item.qty * item.product.price)"></price></b>
								<a href="#" @click.stop="$emit('deleteItem', index)" class="badge badge-danger text-white mx-1">-</a>
							</div>
						</div>
					</div>
				</div>
			</div>
		</nav>
</template>

<script>
import Price from "./Price";
import { FontAwesomeIcon } from "@fortawesome/vue-fontawesome";

export default {
	name: "navbar",
	props:["cart", "cartQty", "cartTotal"],
	components:{
		FontAwesomeIcon,
		Price
	}
}
</script>