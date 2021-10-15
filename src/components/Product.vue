<template>
   <div class="content">
        <div class="img-area">
            <!-- <img :src="imageUrl" :alt="product.title.name" @load="setheight" /> -->
            <img :src="product.image" class="img-before" :alt="product.name" />
            <img :src="product.image2" class="img-after" :alt="product.name" />
            <div class="price">R$ {{ product.price }}</div>
            <p class="description">{{ product.description }}</p>
        </div>
        <div class="text">
            <h2 class="name">{{ product.name }}</h2>
        </div>
        <button class="btn btn-red-line" @click="removeFromCart(product)" v-if="inCart(product)">Remover</button>
		<button class="btn btn-black-line" @click="addToCart(product)" v-else>Comprar</button>
    </div>
</template>

<script>
export default {
    data() {
      	return {}
    },
    props: {
      	product: Object
	},
	created() {},
    computed: {},
	methods: {
        addToCart(product){
            this.$parent.addToCart(product)
		},
		inCart(product){
            return this.$parent.inCart(product)
		},
		removeFromCart(product){
            this.$parent.removeFromCart(product)
		}
    }
  }
</script>
<style lang="scss"></style>