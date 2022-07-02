<template>
  <div class="book">
    <img
      :src="
        book.volumeInfo.imageLinks !== undefined
          ? book.volumeInfo.imageLinks.thumbnail
          : require('../assets/Group.png')
      "
      alt=""
    />
    <div class="infos">
      <p>Tytuł: {{ book.volumeInfo.title }}</p>
      <p>
        Autor:
        {{ book.volumeInfo.authors ? book.volumeInfo.authors[0] : "Nie znany" }}
      </p>
      <p>Data publikacji: {{ book.volumeInfo.publishedDate }}</p>
      <p>E-Book: {{ book.saleInfo.isEbook ? "Tak" : "Nie" }}</p>
      <p>
        Liczba Stron:
        {{
          book.volumeInfo.pageCount ? book.volumeInfo.pageCount : "Nie znana"
        }}
      </p>
      <a :href="book.volumeInfo.canonicalVolumeLink" target="_blank">Więcej</a>
    </div>
  </div>
</template>

<script>
export default {
  props: ["book"],
};
</script>

<style scoped>
@import url("https://fonts.googleapis.com/css2?family=Inter&display=swap");
.book {
  width: calc(28.489583333333336vw - 1.9791666666666665vw * 2);
  height: calc(20.052083333333336vw - 2.2916666666666665vw * 2);
  background-color: #625667;
  border-radius: 8px;

  padding-top: 2.2916666666666665vw;
  padding-bottom: 2.2916666666666665vw;

  padding-left: 1.9791666666666665vw;
  padding-right: 1.9791666666666665vw;
  display: flex;
}
.book img {
  width: 12.291666666666666vw;
  height: 15.46875vw;
  margin: 0;
  margin-right: 1.3541666666666667vw;
}
.infos p {
  margin-bottom: 0.78125vw;
  font-size: 20px;
  color: #fff;
  font-family: "Inter", sans-serif;
}
.infos a {
  color: #fff;
  font-size: 20px;
  text-decoration: none;
  font-family: "Inter", sans-serif;
}
</style>
