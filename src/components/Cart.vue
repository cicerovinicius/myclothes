<template>
    <div id="cart">
		<button class="btn btn-green cart-btn" v-if="!cart.open" @click="showCart(!cart.open)" title="Clique para ver o carrinho">
			<div class="icon"><i class="fas fa-shopping-cart"></i></div>
		</button>
		<!-- <button class="close-cart-btn" v-else @click="showCart(false)" title="Clique para continuar comprando"></button> -->
        <h2 class="title" title="Carrinho de produtos">Carrinho</h2>
        <ul class="cd-cart-items">
            <li v-for="product in cart.products">
				<div class="img">
					<img :src="product.image" :alt="product.name" />
				</div>
				<div class="description">
					<h4 class="name" :title="product.name">{{ product.name }}</h4>
					<span class="cd-price">R$ {{ product.price }}</span>
				</div>
                <button class="btn btn-remove" @click="removeProduct(product)" title="Clique para remover esse item do carrinho">Remove</button>
            </li>
        </ul> 
        <div class="total-cart">
            <p class="total-itens">Total de itens: <span>{{ cart.products.length }}</span></p>
            <p class="total-price">Total: <span>R$ {{ total }}</span></p>
        </div> 
        <button class="btn btn-green btn-checkout" @click="checkout()" title="Clique para finalizar essa compra">Finalizar</button>
    </div>
</template>

<script>
    export default {
        data() {
            return {
				totalPrice: 0
			}
        },
        props: {
            cart: Object
        },
        computed: {
			total: function() {
				let total = 0
				this.cart.products.forEach(product => {
					total += Number(product.price)
				});
				this.cart.total = total
				return total
			}
		},
        methods: {
			removeProduct: function(product){
				let cart = this.cart.products.filter((produto, index) => {
					return product != produto
				})
				this.cart.products = cart
			},
			showCart(active){
				this.$parent.openCart(active);
			},
			checkout(){
				this.cart.checkout = (this.cart.products.length > 0)? true : false;
				this.cart.open = false
			}
		}
    }
</script>
<style lang="scss"></style>