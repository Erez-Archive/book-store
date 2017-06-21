<template>
    <section v-if="books">
        <h2>We have {{books.length}} Books</h2>
        <button @click="isCreateMode=true">+</button>
        <ul>
            <book-preview v-for="currBook in books" @click.native="selectBook(currBook)" @edit="editBook(currBook)" @delete="deleteBook(currBook)" @add="addBook" @substract="substractBook" :book="currBook">
            </book-preview>
        </ul>
        <book-details v-if="selectedBook" @close="resetSelected" @next="selectNext" :book="selectedBook">
        </book-details>
    
        <book-edit v-if="editedBook || isCreateMode" :book="editedBook" @save="saveBook" @cancel="cancelEditBook">
        </book-edit>
    
    </section>
</template>

<script>
import bookService from '../book.service'
import BookPreview from './BookPreview'

export default {
    name: 'book-list',
    components: {
        BookPreview
    },
    created() {
        bookService.getBooks().then(books => this.books = books)
    },
    data() {
        return {
            books: null,
            selectedBook: null,
            editedBook: null,
            isCreateMode: false
        }
    },
    methods: {
        selectBook(book) {
            this.selectedBook = book
        },
        resetSelected() {
            this.selectedBook = null
        },
        selectNext() {
            this.selectedBook = bookService.getNext(this.selectedBook)
        },
        editBook(book) {
            console.log('Editing the book', book)
            this.editedBook = book;
        },
        deleteBook(book) {
            bookService.deleteBook(book);
        },
        saveBook(book) {
            bookService.saveBook(book);
            this.editedBook = null;
            this.isCreateMode = false;
        },
        cancelEditBook() {
            this.editedBook = null;
            this.isCreateMode = false;
        },
        addBook(book) {
            console.log('got book at booklist:', book);
            this.$emit('add', book);
        },
        substractBook(book) {
            console.log('got book to substract at booklist:', book);
            this.$emit('substract', book);
        }
    },
}
</script>

<style scoped>

</style>
