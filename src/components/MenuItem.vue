<template>
	<div class="menu-item">
		<img class="image" :src="image.source" :alt="image.alt" />
		<div>
			<h3>{{ name }}</h3>
				<p v-if="inStock">En stock</p>
				<p v-else>En rupture de stock</p>
				<div>
					<label for="add-item-quantity">Quantité : {{ quantity }}</label>
					<label for="add-item-quantity"> Prix : {{ generatedPrice }}€</label>
					<input v-model.number="quantity" id="add-item-quantity" type="number" />
					<button @click="addToShoppingCart(quantity)">
						Ajouter au panier
					</button>
				</div>
		</div>
	</div>
</template>
<style lang="scss">
		.menu-item {
		display: flex;
		width: 500px;
		justify-content: space-between;
		margin-bottom: 30px;
		}
		.image {
		max-width: 300px;
		}
</style>
<script>
		export default {
		name: 'MenuItem',
		props: ["addToShoppingCart", "image", "inStock", "name", "quantity","prix"],
		data() {
		return {
			onSale: false
		}
	},
	computed: {
		generatedPrice() {
			if (this.onSale) {
				return (this.prix * 0.9).toFixed(2)
			} else {
				return this.prix
			}
		}
	},
	beforeMount() {
		const today = new Date().getDate()
		if (today % 2 === 0) {
			this.onSale = true
		}
	}
		}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->

