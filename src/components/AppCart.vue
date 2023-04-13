<template>
	<div class="cart_wrapper">
		<div class="f">
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
						<td data-label="Название товара">{{ item.product.title }}</td>
						<td data-label="Количество">{{ item.col }}</td>
						<td data-label="Стоимость">{{ item.col * item.product.price }}</td>
					</tr>
				</tbody>
			</table>
		</div>

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
	padding-top: 55px;
	flex-grow: 1;
}
.f {
	display: flex;

	flex-direction: column;
	align-items: center;
	justify-content: space-between;
}
.overf {
	overflow-x: auto;
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

@media (max-width: 500px) {
	.f {
		display: inline-block;
	}
	.cart {
		border-collapse: collapse;
		border-spacing: 0;
	}
	.cart thead {
		display: none;
	}
	.cart tr {
		display: block;

		margin-bottom: 25px;
		border-bottom: 2px solid #ddd;
	}
	.cart tr td:first-child {
		width: 100%;
	}
	.cart td {
		display: flex;
		justify-content: space-between;
		text-align: right;
		border-bottom: 1px dotted #ccc;
		border-right: 1px solid transparent;
	}
	.cart td:before {
		content: attr(data-label);
		text-align: left;
		float: left;
		text-transform: uppercase;
		font-weight: bold;
	}
	.cart__btn {
		width: 100%;
		min-width: auto;
	}
}
</style>
