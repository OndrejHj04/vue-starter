<template>
  <h1 class="bg-red-500">Knihy</h1>
  <div v-for="book in books" :key="book.id">
    <span>{{ book.title }}</span>
  </div>

  <button class="bg-green-500 p-2" @click="handleNew">add new</button>
</template>

<script setup lang="ts">
import { onMounted, ref } from 'vue';


const books = ref([])

const handleNew = () => fetch(import.meta.env.VITE_ROOT_API + '/books', {method: 'POST'}).then(()=>getBooks())

const getBooks = async () => {
  const data = await fetch(import.meta.env.VITE_ROOT_API + '/books')
  const result = await data.json()

  books.value = result
}

onMounted(async ()=>getBooks())
</script>