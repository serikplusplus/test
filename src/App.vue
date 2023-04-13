<template>
	<AppHeader />
	<div class="main container">
		<div class="main__wrapper">
			<AppProductForm @addToCard="addToCard($event)" />
			<AppCart :cart="cart" @clear="clearCart" />
		</div>
	</div>
	<AppFooter />
</template>

<script>
import AppHeader from './components/AppHeader.vue'
import AppProductForm from './components/AppProductForm.vue'
import AppCart from './components/AppCart.vue'
import AppFooter from './components/AppFooter.vue'

export default {
	components: { AppHeader, AppProductForm, AppCart, AppFooter },
	data() {
		return {
			cart: [],
		}
	},
	methods: {
		addToCard(val) {
			console.log(val)
			this.cart.push(val)
		},
		clearCart() {
			this.cart = []
		},
	},
	mounted() {},
}
</script>

<style>
*,
*::after,
*::before {
	box-sizing: border-box;
}
body {
	height: 100vh;
	margin: 0;
	font-family: 'Roboto';
	font-style: normal;
	font-weight: 400;
	font-size: 24px;
	line-height: 28px;
	color: #222222;
}
#app {
	height: 100%;
}
.container {
	max-width: 1400px;
	padding: 0 25px;
	margin: 0 auto;
}
.btn {
	background-color: transparent;
	border: none;
	cursor: pointer;
}
.btn_blue {
	background: #2fa6ea;
	border: 1px solid #000000;
	border-radius: 4px;
	padding: 12px 24px;
	color: #ffffff;
}
.btn_green {
	background: #61a91a;
	border-radius: 4px;
	border: 1px solid #000000;
	padding: 12px 24px;
	color: #ffffff;
}
.main {
	margin-bottom: 50px;
}
.main__wrapper {
	display: flex;

	justify-content: center;
	flex-wrap: wrap;
	gap: 50px;
	padding-top: 25px;
}
</style>
