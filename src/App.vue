<template>
  <div>
    <h2>Book List</h2>
    <div>
      <input type="text" placeholder="ADD YOUR CHOICE" v-model="newBook">
      <button @click="addBook">Add Book</button>
    </div>
    <ul>
      <li v-for="(book, index) in books" :key="index">
        {{ book }}
        <button @click="deleteBook(index)">Delete</button>
      </li>
    </ul>
   
  </div>
</template>

<script setup>
import { ref, onMounted } from 'vue';

const BOOKS_KEY = 'my-books';

const books = ref([]);
const newBook = ref('');

const addBook = () => {
  if (newBook.value) {
    books.value.push(newBook.value);
    newBook.value = '';
    saveBooks();
  }
};

const deleteBook = (index) => {
  books.value.splice(index, 1);
  saveBooks();
};

const saveBooks = () => {
  localStorage.setItem(BOOKS_KEY, JSON.stringify(books.value));
};

const loadBooks = () => {
  const storedBooks = localStorage.getItem(BOOKS_KEY);
  if (storedBooks) {
    books.value = JSON.parse(storedBooks);
  }
};

onMounted(loadBooks);
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #444;
  margin-top: 60px;
}
body {
  font-family: Arial, sans-serif;
  color: #333;
}

/* Style the book list */
ul {
  list-style: none;
  margin: 0;
  padding: 0;
}

li {
  display: flex;
  justify-content: space-around;
  align-items: center;
  /* border-bottom: 1px solid #ccc; */
  padding: 8px;
  
}

li:last-child {
  border-bottom: none;
}

/* Style the input field and button */
input[type="text"] {
  padding: 8px;
  font-size: 16px;
  border: none;
  border: 1px solid #ccc;
  border-radius: 5px;
  outline: none;
}

button {
  margin-left: 30px;
  padding: 8px 16px;
  font-size: 16px;
  background-color: #4caf50;
  color: #fff;
  border: none;
  border-radius: 4px;
  cursor: pointer;
}

button:hover {
  background-color: #3e8e41;
}
 

</style>
