<template>
  <div class="books">
    <found-book
      v-for="book in books"
      :key="book.id ? book.id : Math.random()"
      :book="book ? book : {}"
    ></found-book>
  </div>
</template>

<script>
import FoundBook from "./FoundBook.vue";
export default {
  props: ["books"],
  components: {
    FoundBook,
  },
};
</script>

<style scoped>
::-webkit-scrollbar {
  width: 0px;
}

.books {
  display: flex;
  margin-top: 9.351851851851851vh;
  width: 91.09375vw;
  overflow-y: scroll;
  flex-wrap: wrap;
  column-gap: 2.8125vw;
  row-gap: 2.8125vw;
  height: 28.572917vw;
  scrollbar-width: none;
}
</style>
