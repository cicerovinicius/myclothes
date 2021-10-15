<template>
    <div id="modal" :class="{ open: this.cart.checkout }">
		<button class="close-btn" @click="closeModal()" title="Clique para fechar"></button>
        <h2 class="title">Parabéns, sua compra foi concluída!</h2>
        <p class="description">
            Sua compra no valor de R$ {{ cart.total }} foi concluída com sucesso.<br>
            Ficamos felizes com sua preferência e disponibilizamos aqui um código para que você possa comprar novamente com <b>desconto de 10%</b>:
        </p> 
        <div class="codigo" v-if="this.cart.checkout">{{ generateCode(4) }}10</div>
    </div>
</template>

<script>
	export default {
        data() {
            return {}
        },
        props: {
            cart: Object
        },
		methods:{
			generateCode(len) {
				let text = " "
				let letters = "abcdefghijklmnopqrstuvwxyz"
				for(let i=0; i < len; i++) {
					text += letters.charAt(Math.floor(Math.random() * letters.length))
				}
				return text.toUpperCase();
			},
			closeModal(){
				this.cart.checkout = false
				this.cart.total = 0
				this.cart.products = []
			}
		}
    }
</script>