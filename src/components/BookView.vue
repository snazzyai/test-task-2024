<script setup lang="ts">
import { storeToRefs } from 'pinia';
import BookList from '@/components/BookList.vue'
import BookNew from '@/components/BookNew.vue'
import { useBookStore } from '@/stores/bookStore';

const bookStore = useBookStore()
const { showAddNewBookView } = storeToRefs(bookStore)

function toggleAddBook() {
  showAddNewBookView.value = !showAddNewBookView.value
}


</script>


<template>
  <main class="flex flex-col items-center justify-center px-[20%] py-[5%] mx-auto">
    <section class="w-full px-12 py-12 bg-blue shadow">
      <header>
        <section class="flex flex-row justify-between py-2">
          <h1 class="text-xl font-semibold leading-tight text-gray-900 md:text-2xl">My Book Tracker</h1>
          <button
            class="w-30 bg-green-400 px-10 py-2 rounded-xl text-white bg-blue-700 hover:bg-blue-800 focus:ring-4 focus:ring-blue-300 font-medium me-2 mb-2 focus:outline-none"
            @click="toggleAddBook" v-if="!showAddNewBookView">Add new book</button>
          <button
            class="w-30 bg-green-400 px-5 py-2 rounded-xl text-white bg-blue-700 hover:bg-blue-800 focus:ring-4 focus:ring-blue-300 font-medium me-2 mb-2 focus:outline-none"
            @click="toggleAddBook" v-if="showAddNewBookView">X</button>
        </section>
      </header>
      <section v-if="showAddNewBookView">
        <BookNew />
      </section>

      <section>

        <div>
          <p class="py-2 font-semilight text-bermuda-gray-700">Highest number of Pages read: <span class="font-light">{{
            bookStore.totalPagesRead }}</span></p>
          <p class="py-2 font-semilight text-bermuda-gray-700">Popular genres you are reading: </p>
          <div v-for="genre in bookStore.popularGenres" :key="genre" class="font-semibold text-bermuda-gray-700">
            <p class="italic font-light">{{ genre }}</p>
          </div>
        </div>
        <div class="flex flex-row justify-center">
          <h1 class="text-2xl leading-tight font-semibold text-bermuda-gray-700 md:text-2xl py-4">My Book List</h1>
          <p class="text-red-400" v-if="bookStore.Books.length <= 0">No books added yet!</p>
        </div>
        <Suspense>
          <BookList />
          <template #fallback>
            <div>Loading...</div>
          </template>
        </Suspense>
      </section>
      <section>
        <h1 class="text-2xl font-semibold leading-tight text-bermuda-gray-700 md:text-xl">Completed Books</h1>
        <div v-for="book in bookStore.completedBooks" :key="book.id" class="font-semibold text-bermuda-gray-700">
          <p class="italic font-light">{{ book.title }}</p>
        </div>
      </section>

    </section>

  </main>
</template>