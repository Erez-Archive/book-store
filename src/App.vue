<template>
  <div id="app">
    <img src="./assets/logo.png">
    <router-view></router-view>
  
    <div class="inline-flex">
      <book-list @add="addBook" @substract="substractBook"></book-list>
      <cart></cart>
    </div>
  </div>
</template>

<script>
import BookList from './components/BookList'

import cartService from './cart.service'
import Cart from './components/Cart'
export default {
  name: 'app',
  components: {
    BookList,
    Cart,
  },
  methods: {
    addBook(book) {
      console.log('Book arrived all the way up:', book)
      cartService.addToCart(book)
    },
    substractBook(book) {
      console.log('Book to substract arrived all the way up:', book)
      cartService.substractFromCart(book.id)
    }
  }
}

</script>

<style scoped>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;

  background: lightgray;
}
  .inline-flex {
    display: inline-flex;
  }
</style>
