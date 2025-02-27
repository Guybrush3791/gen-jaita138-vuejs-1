<template>
  <div v-if="newBook">
    <h1>
      <button @click="createBook(null)">
        <span style="font-size: 1em">&#x2717;</span>
      </button>
      Create Book
    </h1>
    <form @submit.prevent="onSubmit">
      <input type="text" placeholder="Title" v-model="newBook.title" />
      <br />
      <input type="text" placeholder="ISBN" v-model="newBook.isbn" />
      <br />
      <input type="text" placeholder="Year" v-model="newBook.year_pub" />
      <br />
      <select v-model="newBook.author">
        <option v-for="author in authors" :key="author.id" :value="{ id: author.id }">
          {{ author.name }} {{ author.surname }} ({{ author.nationality }})
        </option>
      </select>
      <br />
      <h3>Genres</h3>
      <div v-for="genre in genres" :key="genre.id">
        <input type="checkbox" :value="{ id: genre.id }" v-model="newBook.genres" />
        <label>{{ genre.name }}</label>
      </div>
      <button type="submit" @click="storeBook">Save</button>
    </form>
    <h3>DEBUG:</h3>
    <pre>{{ newBook }}</pre>
  </div>
  <div v-else>
    <h1>
      <button @click="createBook(emptyBook)">
        <span style="font-size: 1em">&#x271A;</span>
      </button>
      Books
    </h1>
    <div>
      <p v-for="book in books" :key="book.id">
        <button @click="selectBook(book)">
          <span style="font-size: 1em">&#x2713;</span>
        </button>
        {{ book.title }} ({{ book.author.name }}) - {{ book.year_pub }}
      </p>
    </div>
    <div v-if="selectedBook">
      <br />
      <hr />
      <br />
      <h2>
        <button @click="selectBook(null)">
          <span style="font-size: 1em">&#x2717;</span>
        </button>
        Book details
      </h2>
      <ul>
        <li>Id: {{ selectedBook.id }} (ISBN: {{ selectedBook.isbn }})</li>
        <li>Title: {{ selectedBook.title }}</li>
        <li>
          Author: {{ selectedBook.author.name }} {{ selectedBook.author.surname }} ({{
            selectedBook.author.nationality
          }})
        </li>
        <li>Year: {{ selectedBook.year_pub }}</li>
        <li v-if="selectedBook.genres.length > 0">
          Genres:
          <ul>
            <li v-for="genre in selectedBook.genres" :key="genre.id">
              {{ genre.name }}
            </li>
          </ul>
        </li>
      </ul>
    </div>
  </div>
</template>

<script setup>
import { onMounted, ref } from 'vue'
import axios from 'axios'

const emptyBook = {
  genres: [],
}

const books = ref([])
const authors = ref([])
const genres = ref([])

const selectedBook = ref(null)

const newBook = ref(null)

const init = async () => {
  const resBook = await axios.get('http://localhost:8080/api/v1/book')
  const resAuthor = await axios.get('http://localhost:8080/api/v1/author')
  const resGenre = await axios.get('http://localhost:8080/api/v1/genre')

  const dataBook = resBook.data
  const dataAuthor = resAuthor.data
  const dataGenre = resGenre.data

  books.value = dataBook
  authors.value = dataAuthor
  genres.value = dataGenre
}
const selectBook = (book) => {
  selectedBook.value = book
  console.log('selectedBook', selectedBook.value)
}
const createBook = (book) => {
  if (book == null) {
    newBook.value = null
    return
  }

  newBook.value = { ...book }
}
const storeBook = async () => {
  await axios.post('http://localhost:8080/api/v1/book', newBook.value)

  createBook(null)
  init()
}

onMounted(init)
</script>

<!--

  - vedere tutti i dettagli di un singolo libro
  - creare un nuovo libro
  - modificare tutti i dettagli di un singolo libro
  - eliminare un libro

  # bonus
  - crud di autore
  - crud di genere

-->
