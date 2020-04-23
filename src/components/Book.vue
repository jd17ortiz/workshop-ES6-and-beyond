<template>
  <div class="book">
    <div class="book-thumb">
      <img v-bind:src="book.volumeInfo.imageLinks.thumbnail" alt>
    </div>
    <div class="book-content">
      <h3 class="book-title">{{ book.volumeInfo.title }}</h3>
      <div class="book-author">
        By
        <strong>{{ book.volumeInfo.authors[0] }}</strong>
      </div>
      <div class="book-description">{{ book.volumeInfo.description | truncate }}</div>
    </div>
  </div>
</template>

<script>
export default {
  name: "Book",
  props: {
    book: {
      type: Object,
      required: true
    }
  },
  filters: {
    truncate(value) {
      console.log(value);
      if (!value) return "";
      const newline = value.indexOf(".");
      return newline > 0 ? value.slice(0, newline) : value;
    }
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.book {
  margin-bottom: 25px;
  display: block;
}

.book-thumb,
.book-content {
  display: inline-block;
  vertical-align: top;
  margin-right: -0.25em;
}

.book-thumb {
  width: 128px;
  position: relative;
  transform: perspective(100px) rotateY(-3deg);
}

.book-thumb::before,
.book-thumb::after {
  content: "";
  position: absolute;
  top: 2%;
  height: 96%;
  z-index: -1;
}

.book-thumb::before {
  background-color: #5a2d18;
  width: 100%;
  left: 7.5%;
  box-shadow: 5px 5px 20px #333;
}

.book-thumb::after {
  background-color: #e5e5e5;
  width: 5%;
  left: 100%;
  box-shadow: inset 0 0 5px #aaa;
  transform: perspective(100px) rotateY(20deg);
}

.book-author {
  margin-bottom: 10px;
}

.book-content {
  overflow: hidden;
  padding-left: 30px;
  width: calc(100% - 200px);
}

.book-title {
  margin: 0 0 10px;
  line-height: 1.1;
}
</style>
