<template>
	<div class="cart_wrapper">
		<table class="cart">
			<thead class="cart__head">
				<tr>
					<td>Название товара</td>
					<td>Количество</td>
					<td>Стоимость</td>
				</tr>
			</thead>

			<tbody>
				<tr v-for="item in cart" :key="item.id">
					<td>{{ item.product.title }}</td>
					<td>{{ item.col }}</td>
					<td>{{ item.col * item.product.price }}</td>
				</tr>
			</tbody>
		</table>
		<div class="full__price">Итого: {{ fullPrice }}</div>
		<button class="btn btn_green cart__btn" @click="send">Сохранить</button>
	</div>
</template>

<script>
import axios from 'axios'
export default {
	props: ['cart'],
	data() {
		return {}
	},
	methods: {
		send() {
			let pr = []
			this.cart.forEach(element => {
				pr.push({ product_id: element.product.id, quantity: element.col })
			})

			axios
				.post('https://dev-su.eda1.ru/test_task/save.php', JSON.stringify(pr))
				.then(() => {
					this.$emit('clear')
				})
		},
	},
	computed: {
		fullPrice() {
			let price = 0
			this.cart.forEach(element => {
				price += element.col * element.product.price
			})
			return price
		},
	},
}
</script>

<style scoped>
.cart_wrapper {
	display: flex;
	flex-grow: 1;
	flex-direction: column;
	align-items: center;
	justify-content: space-between;
	padding-top: 55px;
}
.cart {
	width: 100%;
	min-height: 400px;
	border-bottom: 1px solid #2fa6ea;
	margin-bottom: 25px;
}
.cart__head {
	color: #0170ae;
}
.cart tr {
	display: flex;
	gap: 50px;
}
.cart tr td {
	flex-grow: 1;
}
.cart tr td:first-child {
	width: 50%;
}
.cart__btn {
	min-width: 395px;
}
.full__price {
	align-self: flex-end;
	margin-bottom: 25px;
}
</style>
