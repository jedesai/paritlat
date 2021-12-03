<template>
  <div>
    <div class="heading">
      <h2 class="p-2 text-center">Students List</h2>
    </div>
    <hr />
    <div class="col-md-12">
      <div class="row">
        <div v-bind:key="book.id" v-for="book in books" class="col-md-6 mb-2">
          <div class="card">
            <div class="card-body">
              <BookItem
                v-bind:book="book"
                v-on:del-book-item="delBookMethod"
                v-on:edit-book-item="editBookMethod"
              />
            </div>
          </div>
        </div>
      </div>
    </div>

    <div v-if="!books.length">
      <p>No student Information to display!!</p>
    </div>
  </div>
</template>

<script>
import BookItem from "./BookItem";
export default {
  name: "Books",
  props: ["books"],
  components: {
    BookItem,
  },
  methods: {
    delBookMethod(id) {
      //send to parent
      this.$emit("del-book-event", id);
    },
    editBookMethod(id) {
      //send to parent (App.vue)
      this.$emit("edit-book-event", id);
    },
  },
};
</script>

<style scoped></style>
