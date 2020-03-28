<template>
	<transition-group name="fade" tag="div"
		enter-active-class="animated fadeInRight"
		leave-active-class="animated fadeOutRight" >
		<!-- if statement inside for loop -->
		<div v-for="(item, index) in products" :key="item.id">
			<div class="row d-flex mb-3 align-items-center" 
				v-if="item.price<=Number(maximum)"
				:data-index="index">
			<div class="col-1 m-auto">
			<button class="btn btn-info" @click="$emit('add', item)">+</button> 
			</div>
			<div class="col-4">
				<img class="img-fluid d-block" :src="item.image" :alt="item.name">
			</div>
			<div class="col">
				<h3 class="text-info">{{ item.name }}</h3>
				<p class="mb-0">{{ item.description }}</p>
				<div class="h5 float-right">
					<price :value="Number(item.price)"></price></div>     
				</div>
			</div>
		</div>
	</transition-group>
</template>


<script>
import Price from "./Price";

export default {
	name: "product-list",
	components: {
		Price
	},
	props: ["products", "maximum"]
}
</script>