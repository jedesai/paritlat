<template>
  <div>
    <h2 class="p-2 text-center">Student Form</h2>
    <hr />
    <form @submit="addBook">
      <div class="form-group">
        <label for="exampleInputPassword1" class="mr-2">First Name</label>
        <input
          class="form-control form-control-sm"
          type="text"
          name="firstName"
          v-model="firstName"
          placeholder="Type First Name"
        />
      </div>
      <div class="form-group">
        <label for="exampleInputPassword1" class="mr-2">Last Name</label>
        <input
          class="form-control form-control-sm"
          type="text"
          name="lastName"
          v-model="lastName"
          placeholder="Type Last Name"
        />
      </div>
      <div class="form-group">
        <label for="exampleInputPassword1" class="mr-2">Email</label>
        <input
          class="form-control form-control-sm"
          type="text"
          name="email"
          v-model="email"
          placeholder="Type Email"
        />
      </div>
      <div class="form-group">
        <label for="exampleInputPassword1" class="mr-2">Mobile</label>
        <input
          class="form-control form-control-sm"
          type="text"
          name="mobile"
          v-model="mobile"
          placeholder="Type Mobile"
        />
      </div>
      <div class="form-group">
        <label for="exampleInputPassword1" class="mr-2">Website</label>
        <input
          class="form-control form-control-sm"
          type="text"
          name="website"
          v-model="website"
          placeholder="Type Website Url"
        />
      </div>

      <div class="submitButton">
        <input type="submit" value="Submit" class="btn btn-sm btn-success" />
      </div>
    </form>
  </div>
</template>

<script>
export default {
  name: "AddBookItem",
  props: ["editBook"],
  data() {
    return {
      // title: "",
      id: "",
      firstName: "",
      lastName: "",
      mobile: "",
      email: "",
      website: "",

      edit: false,
    };
  },
  methods: {
    addBook(e) {
      e.preventDefault();
      if (this.edit === false) {
        // add new book
        const newBook = {
          // title: this.title,
          id: Math.floor(Math.random() * 100),
          firstName: this.firstName,
          lastName: this.lastName,
          mobile: this.mobile,
          email: this.email,
          website: this.website,
        };
        // if (newBook.title !== "") {
        //   this.$emit("add-book-event", newBook);
        if (newBook.id !== "") {
          this.$emit("add-book-event", newBook);
        }
        // this.title = "";
        this.firstName = "";
        this.lastName = "";
        this.mobile = "";
        this.email = "";
        this.website = "";
      } else {
        //edit book
        const bookItem = {
          title: this.title,
          id: this.id,
          firstName: this.firstName,
          lastName: this.lastName,
          mobile: this.mobile,
          email: this.email,
          website: this.website,
        };
        //send to parent (App.vue)
        this.$emit("edit-book-event", bookItem);
        // clear input field
        // this.title = "";
        this.firstName = "";
        this.lastName = "";
        this.mobile = "";
        this.email = "";
        this.website = "";
        this.edit = false;
      }
    },
  },
  watch: {
    editBook: {
      handler() {
        // this.title = this.editBook.title;
        this.id = this.editBook.id;
        this.firstName = this.editBook.firstName;
        this.lastName = this.editBook.lastName;
        this.mobile = this.editBook.mobile;
        this.email = this.editBook.email;
        this.website = this.editBook.website;
        this.edit = true;
      },
      deep: true,
    },
    title: {
      handler() {
        if (this.id === "") {
          this.edit = false;
        }
      },
    },
  },
};
</script>

<style scoped>
label {
  font-weight: 600;
}
</style>
