<template>
  <div id="app">
    <Book v-for="book in books" :book="book" :key="book.id"/>
  </div>
</template>

<script>
import Book from "./components/Book";

export default {
  name: "App",
  components: {
    Book
  },
  data() {
    return {
      books: []
    };
  },
  created() {
    this.fetchBooks("scifi");
  },
  methods: {
    async fetchBooks(volumns) {
      const googleapis = `https://www.googleapis.com/books/v1/volumes?q=volumns:${volumns}&maxResults=15`;
      const res = await fetch(googleapis);
      const data = await res.json();
      this.books = data.items.map(item => {
        item.volumeInfo.imageLinks.thumbnail = item.volumeInfo.imageLinks.thumbnail.replace(
          "http://",
          "https://"
        );
        return item;
      });
    }
  }
};
</script>

<style>
body {
  background: #f9fcfe;
}

#app {
  max-width: 30em;
  margin: 1.5rem auto;
}
</style>
