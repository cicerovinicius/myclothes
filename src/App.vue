<template>
  	<div id="app">
		<div class="topo">
			<div class="container">
				<a href="/" class="logo" title="My Clothes">
					<img src="./assets/images/myclothes-logo.jpg" title="MyClothes" alt="logo preto da loja com um 'Y' em cima de um 'M' e 'Clothes' abaixo" />
				</a>
				<button class="btn cart" :class="{ 'add-product': addedCart }" @click="openCart(true)" title="Clique para abrir o carrinho">
					<i class="icon">
						<img src="./assets/images/black-cart.gif" class="img-before" alt="imagem animada de carrinho em contorno preto" />
						<img src="./assets/images/black-cart.png" class="img-after" alt="carrinho em contorno preto" />
					</i>
					<div class="number" v-if="cart.products.length > 0">{{ cart.products.length }}</div>
				</button>
			</div>
		</div>
		<div class="container">
			<div class="produtos" v-if="products.length">
				<div class="produto" v-for="product in products" :key="product.id">
					<Product :product="product"></Product>
				</div>
			</div>
		</div>
		<Cart :cart="cart" :class="{ 'open': cart.open }"></Cart>
		<Modal :cart="cart"></Modal>
		<div id="backdrop" :class="{ 'cart-opened': (cart.open || cart.checkout) }" @click="openCart(false)">
			<button class="close" v-if="cart.open" @click="showCart(false)" title="Clique para fechar o carrinho"></button>
		</div>
		<div class="footer">
			<div class="container">
				<p>Desenvolvido por @cicerovinicius</p>
				<ul>
					<li>
						<a href="https://github.com/cicerovinicius" class="github" title="Clique para acessar o github">
							<i class="fab fa-github-alt icon"></i>
						</a>
					</li>
					<li>
						<a href="https://www.linkedin.com/in/cicerovinicius/" class="linkedin" title="Clique para acessar o linkedin">
							<i class="fab fa-linkedin-in icon"></i>
						</a>
					</li>
				</ul>
			</div>
		</div>
  	</div>
</template>

<script>
import axios from 'axios';
import Product from './components/Product.vue';
import Cart from './components/Cart.vue';
import Modal from './components/Modal.vue';

export default {
	name: 'app',
	data () {
		return {
			addedCart: false,
			products: [],
			cart: {
				open: false,
				checkout: false,
				products: [],
				total: 0
			}
		}
	},
	components: {
		Product, Cart, Modal
	},
	mounted () {
		axios.get('./src/data/produtos.json').then(response => {
			this.products = response.data.produtos
		})
	},
	methods: {
		addToCart(product){
			this.cart.products.push(product)
			this.addedCart = true;
			setInterval(() => {
				this.addedCart = false;
			}, 1000);
		},
		inCart(product){
			return this.cart.products.indexOf(product) != -1
		},
		removeFromCart(product){
			let cart = this.cart.products.filter((produto, index) => {
				return product != produto
			})
			this.cart.products = cart
		},
		openCart(active){
			this.cart.open = active;
		}
	}
}
</script>
<style lang="scss">
    @import './style.scss';
</style>