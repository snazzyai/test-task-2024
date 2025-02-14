<script setup lang="ts">
import { onMounted } from 'vue'
import { useBookStore } from '@/stores/bookStore'
import { storeToRefs } from 'pinia'
// import type { Book } from '@/types/Books/Book'
import BookReview from '@/components/BookReview.vue';
import BookReadingProgress from './BookReadingProgress.vue';


const bookStore = useBookStore()
const { Books } = storeToRefs(bookStore)


function calculatePercentageRead(read: string, count: string) {
    let convertedRead = parseInt(read)
    let convertedCount = parseInt(count)
    if (convertedRead <= 0) {
        return 0
    }
    if (convertedRead > 0) {
        return Math.floor((convertedRead / convertedCount * 100))
    }
}

onMounted(async () => {
    await bookStore.getAllBooks()
})

</script>


<template>
    <section v-for="book in Books" :key="book.id"
        class="max-w-sm font-semibold bg-white  border-gray-200 rounded-lg shadow py-4 px-5 my-4 mx-auto">
        <section class="p-5">
            <div>
                <p class="mb-2 text-xl font-bold tracking-tight text-gray-500">{{ book.title }}</p>
                <p class="font-medium">Genre: {{ book.genre }}</p>
            </div>
            <div>
                <BookReadingProgress :bookId="book.id" :pageCount="book.pageCount" />
            </div>
            <p class="text-md text-bermuda-gray-600">{{ parseInt(book.pagesRead) }} pages of {{ parseInt(book.pageCount) }}
                read</p>
            <div>
                <span class="pr-3 text-bermuda-gray-700">Status:</span>
                <span v-if="parseInt(book.pageCount) - parseInt(book.pagesRead)" class="text-red-400">Not Completed</span>
                <span v-else class="text-green-500 ">Completed</span>
            </div>

            <div class="py-2">
                <div class="w-full bg-bermuda-gray-200 rounded-full">
                    <div class="bg-green-400 text-xs font-medium text-blue-100 text-center p-0.5 leading-none rounded-full"
                        :style="`width: ${calculatePercentageRead(book.pagesRead, book.pageCount)}%`">
                        <span>{{ calculatePercentageRead(book.pagesRead, book.pageCount) }}%</span>
                    </div>
                </div>
            </div>
            <div>
                <p class="text-sm text-green-500">You have only {{ parseInt(book.pageCount) - parseInt(book.pagesRead) }}
                    pages left to read</p>
            </div>
            <BookReview :bookId="book.id" :pagesRead="book.pagesRead" :pageCount="book.pageCount" :reviews="book.reviews" />
        </section>
    </section>
</template>