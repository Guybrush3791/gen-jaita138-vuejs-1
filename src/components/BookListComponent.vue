<template>
  <h1>Books</h1>
  <p v-for="book in books" :key="book.id">
    {{ book.title }} ({{ book.author.name }}) - {{ book.year_pub }}
  </p>
</template>

<script setup>
import { onMounted, ref } from 'vue'
import axios from 'axios'

const books = ref([])
const init = async () => {
  const res = await axios.get('http://localhost:8080/api/v1/book')
  const data = res.data
  console.log('books', data)

  books.value = data
}
onMounted(init)
</script>
