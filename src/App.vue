<template>
  <div id="app">
    <h1 class="p-2 text-center bg-success text-white">Student Directory</h1>
    <div class="col-md-12">
      <div class="row">
        <div class="col-md-4 border-right">
          <AddBookItem
            v-on:add-book-event="addBookItem"
            v-on:edit-book-event="editBookItemEvent"
            v-bind:editBook="editBook"
          />
        </div>
        <div class="col-md-8">
          <Books
            v-bind:books="books"
            v-on:del-book-event="deleteBookItem"
            v-on:edit-book-event="editBookItem"
          />
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import Books from "./components/Books";
import AddBookItem from "./components/AddBookItem";

export default {
  name: "App",
  components: {
    Books,
    AddBookItem,
  },
  data() {
    return {
      books: [],
      editBook: {
        id: "",
        firstName: "",
        lastName: "",
        email: "",
        mobile: "",
        website: "",
      },
    };
  },
  methods: {
    addBookItem(newBook) {
      // console.log('newbook', newBook.title);
      this.books = [...this.books, newBook];
      // this.books.unshift(newBook)
    },
    deleteBookItem(id) {
      this.books = this.books.filter((book) => book.id !== id);
    },
    editBookItem(id) {
      //find the index of the book's id
      let objIndex = this.books.findIndex((obj) => obj.id === id);
      this.editBook.id = id;
      this.editBook.firstName = this.books[objIndex].firstName;
      this.editBook.lastName = this.books[objIndex].lastName;
      this.editBook.email = this.books[objIndex].email;
      this.editBook.mobile = this.books[objIndex].mobile;
      this.editBook.website = this.books[objIndex].website;
    },
    editBookItemEvent(bookItem) {
      //find the index of this id's object
      let objIndex = this.books.findIndex((obj) => obj.id === bookItem.id);
      //update the item
      this.books[objIndex].firstName = bookItem.firstName;
      this.books[objIndex].lastName = bookItem.lastName;
      this.books[objIndex].email = bookItem.email;
      this.books[objIndex].mobile = bookItem.mobile;
      this.books[objIndex].website = bookItem.website;
    },
  },
  watch: {
    books: {
      handler() {
        localStorage.setItem("books", JSON.stringify(this.books));
      },
      deep: true,
    },
  },
  mounted() {
    if (localStorage.getItem("books")) {
      this.books = JSON.parse(localStorage.getItem("books"));
    }
  },
};
</script>

<style>
* {
  box-sizing: border-box;
  padding: 0;
  margin: 0;
}
#app {
  background-color: #c6f4d0;
  min-height: 100vh;
}
</style>
