<template>
  <div class="">
    <p class="mb-1 row">
      <strong class="col-md-3">Name:</strong> {{ book.firstName }}
      {{ book.lastName }}
    </p>
    <p class="mb-1 row">
      <strong class="col-md-3">Email:</strong> {{ book.email }}
    </p>
    <p class="mb-1 row">
      <strong class="col-md-3">Mobile:</strong> {{ book.mobile }}
    </p>
    <p class="mb-1 row">
      <strong class="col-md-3">Website:</strong> {{ book.website }}
    </p>

    <div class="mt-2">
      <button
        type="button"
        class="btn btn-sm btn-success mr-2"
        @click="$emit('edit-book-item', book.id)"
      >
        Edit
      </button>
      <button
        type="button"
        class="btn btn-sm btn-danger"
        @click="$emit('del-book-item', book.id)"
      >
        Delete
      </button>
    </div>
  </div>
</template>

<script>
export default {
  name: "BookItem",
  props: ["book"],
};
</script>

<style scoped>
strong {
  font-weight: 600;
}
</style>
