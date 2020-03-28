<template>
	<transition name="custom" 
		enter-active-class="animated fadeInLeft"
		leave-active-class="animated fadeOutRight">
		<div v-if="sliderStatus">
			<div class="align-items-center" :class="sliderState">
				<label for="formMax" class="font-weight-bold mr-2" >Max</label>
				<input type="text" 
					id="formMax" class="form-control mx-2 text-center" 
					style="width:60px;" v-model="maxAmount"
					@change="$emit('upadteMaximum', maxAmount)"
					>
				<input type="range" class="custom-range mx-2" min="0" max="200" 
					v-model="maxAmount "
					@input="$emit('upadteMaximum', maxAmount)">
			</div>
		</div>
	</transition>
</template>

<script>
export default {
	name: "price-slider",
	data: function(){
		return {
			maxAmount: 99
		}
	},
	props: ['sliderStatus'],
	computed: {
		sliderState: function(){
			return this.sliderStatus ? 'd-flex' : 'd-none';
		}
	}
}
</script>

<style scoped>
	.fade-enter, .fade-leave-to {
		opacity: 0;
	}

	.fade-enter-active, .fade-leave-active{
		transition: all .5s ease-in-out;
	}		

</style>