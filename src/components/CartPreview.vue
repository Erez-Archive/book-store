<template>
    <li class="cart-preview">
        <h2>{{item.title}}</h2>
        <h2>Quantity: {{item.quantity}}</h2>
        <h3>Price: \${{item.price * item.quantity}}</h3>
        <button @click.stop="clearItem">x</button>
    </li>
</template>

<script>
export default {
    name: 'cart-preview',
    props: ['item'],
    methods: {
        clearItem() {
            console.log('Request Product Clearing');
            this.$emit('clear');
        }
    }
}
</script>

<style composed>

</style>


