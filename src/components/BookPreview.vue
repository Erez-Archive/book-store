<template>
    <li class="book-preview">
        <h2>{{book.title}}</h2>
        <img src="http://via.placeholder.com/250x150">
        <h3>\${{book.price}}</h3>
        <button @click.stop="editBook">&#9998;</button>
        <button @click.stop="deleteBook">x</button>
        <button @click.stop="addToCart">+</button>
        <button @click.stop="substractFromCart">-</button>
    </li>
</template>

<script>
import BookDetails from './BookDetails'
export default {
    name: 'book-preview',
    components: {
        BookDetails
    },
    props: ['book'],
    methods: {
        editBook() {
            console.log('Request Edit');
            this.$emit('edit');
        },
        deleteBook() {
            console.log('Request Delete');
            this.$emit('delete');
        },
        addToCart() {
            console.log('Please add book to cart');
            this.$emit('add', this.book);
        },
        substractFromCart() {
            console.log('Please remove book from cart');
            this.$emit('substract', this.book);
        }
    }
}
</script>

<style scoped>
.book-preview {
    list-style: none;
    display: inline-block;
    margin: 5px;
    padding: 10px;
    border: 1px solid gray;
    background: lightgray;
    text-align: center;
}
</style>


