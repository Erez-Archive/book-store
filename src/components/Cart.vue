<template>
    <section class="cart">
        <h1> Your Cart </h1>
        <h2>Cart Total: {{getTotal()}}$</h2>
        <ul v-if="cartItems.length">
            <cart-preview v-for="item in cartItems" @clear="clearCartItem(item)" :item="item">
            </cart-preview>
        </ul>
    </section>
</template>

<script>
import cartService from '../cart.service'
import CartPreview from './CartPreview'
export default {
    name: 'cart',
    components: {
        CartPreview
    },
    created() {
        this.cartItems = cartService.getCartItems();
    },
    data() {
        return {
            cartItems: null
        }
    },
    methods: {
        getTotal() {
            return cartService.getCartTotal();
        },
        clearCartItem(item) {
            cartService.clearItem(item.id);
        }
    }
}
</script>

<style scoped>

</style>


