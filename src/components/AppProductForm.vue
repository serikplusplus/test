<template>
	<form class="product-form" @submit.prevent>
		<label class="product-form__label">
			Выберите продукцию
			<div
				:class="['itc-select', { 'itc-select_show': isDropDawn }]"
				id="select-1"
			>
				<!-- Кнопка для открытия выпадающего списка -->
				<button
					type="button"
					class="itc-select__toggle"
					name="car"
					value=""
					data-select="toggle"
					data-index="1"
					@click="dropDawn"
				>
					{{ product.title }}
				</button>
				<!-- Выпадающий список -->
				<div class="itc-select__dropdown">
					<ul class="itc-select__options">
						<li
							v-for="prod in products"
							:key="prod.id"
							class="itc-select__option"
							data-select="option"
							data-value="volkswagen"
							data-index="0"
							@click="product = prod"
						>
							{{ prod.title }}
						</li>
					</ul>
				</div>
			</div>
		</label>
		<label class="product-form__label">
			Введите количество
			<input
				type="number"
				name="col"
				id="col"
				v-model="col"
				class="product-form__input"
			/>
		</label>
		<button class="btn btn_blue product-form__btn" @click="addToCard">
			Добавить
		</button>
	</form>
</template>

<script>
import axios from 'axios'
export default {
	data() {
		return {
			isDropDawn: false,
			product: {},
			col: 0,
		}
	},
	methods: {
		async getProducts() {
			await axios
				.get('https://dev-su.eda1.ru/test_task/products.php')
				.then(res => {
					this.products = res.data.products
					this.isDownload = true
					this.product = res.data.products[0]
				})
		},
		dropDawn() {
			this.isDropDawn = !this.isDropDawn
		},
		addToCard() {
			this.$emit('addToCard', { product: this.product, col: this.col })

			this.col = 0
		},
	},
	mounted() {
		this.getProducts()
	},
}
</script>

<style scoped>
.product-form {
	display: flex;
	flex-direction: column;
	gap: 35px;
	max-width: 100%;
}
.product-form__label {
	display: flex;
	flex-direction: column;
	gap: 20px;
	color: #222222;
}
.product-form__input {
	background: #eef8ff;
	color: #0170ae;
	padding: 12px 16px;
	border: none;
	border-bottom: 1px solid #2fa6ea;
	font: inherit;
}

.itc-select {
	position: relative;
}
.itc-select__toggle {
	display: flex;
	justify-content: space-between;
	align-items: center;
	width: 100%;
	padding: 12px 16px;
	color: #0170ae;
	cursor: pointer;
	user-select: none;
	font: inherit;

	background: #eef8ff;
	border: 1px solid #000000;
	box-shadow: 0px 4px 4px rgba(0, 0, 0, 0.25);
	border-bottom: 1px solid #2fa6ea;
}
.itc-select__toggle::after {
	flex-shrink: 0;
	width: 22px;
	height: 11px;
	margin-left: 1rem;
	background-image: url('@/assets/dropDawnArrow.svg');
	background-size: cover;
	content: '';
}
.itc-select_show .itc-select__dropdown {
	display: block;
}
.itc-select_show .itc-select__toggle::after {
	transform: rotate(180deg);
}
.itc-select__dropdown {
	position: absolute;
	top: 2.5rem;
	right: 0;
	left: 0;
	z-index: 2;
	display: none;
	max-height: 10rem;
	overflow-y: auto;
	background-color: #fff;
	border: 1px solid #ccc;
	border-radius: 0.3125rem;
}
.itc-select__options {
	margin: 0;
	padding: 0;
	list-style: none;
}
.itc-select__option {
	padding: 0.375rem 0.75rem;
}
.itc-select__option:hover {
	background-color: #f5f5f5;
	cursor: pointer;
	transition: 0.2s background-color ease-in-out;
}
</style>
