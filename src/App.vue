<template>
  <div class="container">
    <h1>Znajdź książkę</h1>
    <div class="search">
      <font-awesome-icon icon="fa-solid fa-magnifying-glass" />
      <input
        type="text"
        placeholder="Wpisz autora, tytuł..."
        v-model="searchInput"
        @keyup="findBook"
      />
    </div>
    <img src="./assets/amico.png" alt="" v-if="search.length === 0" />
    <h2 v-else-if="search.length !== 0 && books.length === 0">
      Wyszukiwanie...
    </h2>
    <found-books v-else :books="books"></found-books>
  </div>
</template>

<script>
import FoundBooks from "./components/FoundBooks.vue";
export default {
  name: "App",
  components: { FoundBooks },
  data() {
    return {
      searchInput: "",
      search: "",
      timer: null,
      books: {},
    };
  },
  methods: {
    findBook() {
      if (this.timer) {
        clearTimeout(this.timer);
        this.timer = null;
      }
      this.timer = setTimeout(() => {
        this.books = [];
        this.search = this.searchInput;
        let books = [];
        if (this.search !== "") {
          fetch(
            "https://www.googleapis.com/books/v1/volumes?q=" +
              this.search +
              "&maxResults=40&orderBy=relevance"
          )
            .then((response) => {
              return response.json();
            })
            .then((data) => {
              data.items.forEach((element) => {
                books.push(element);
              });
              this.books = books;
              console.log(books);
            });
        }
      }, 500);
    },
  },
};
</script>

<style>
@import url("https://fonts.googleapis.com/css2?family=Joti+One&display=swap");

* {
  margin: 0;
}

#app {
  background-color: #4f4355;
  width: 100%;
  height: 100vh;
  background-image: url("./assets/Vector.png");
  background-repeat: no-repeat;
  background-position: bottom;
  background-size: 100%;
  overflow-y: hidden;
}

.container {
  display: flex;
  flex-direction: column;
  align-items: center;
}
.container h1 {
  font-family: "Joti One", cursive;
  font-size: 5.188rem;
  color: #f5f5f5;
  text-shadow: 7px 9px 0px #381f3c;
  margin-top: 7.407407407407407vh;
}
h2 {
  font-family: "Joti One", cursive;
  font-size: 5.188rem;
  color: #f5f5f5;
  text-shadow: 7px 9px 0px #381f3c;
  margin-top: 15.407407407407407vh;
}
.container input {
  border: 0;
  color: #423f44;
  font-size: 22px;
  outline: none;
  background: transparent;
  height: 100%;
}
.container svg {
  color: #423f44;
  font-size: 22px;
  margin-right: 0.5208333333333333vw;
}
.container .search {
  padding: 15px;
  background-color: #f5f5f5;
  border-radius: 13px;
  margin-top: 5vh;
  width: 25%;
}
.container img {
  margin-top: 9.351851851851851vh;
  height: 38.7962962962963vh;
}
</style>

