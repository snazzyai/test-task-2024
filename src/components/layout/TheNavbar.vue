<script setup lang="ts">
import { useRouter } from 'vue-router'
import { useAuthStore } from '@/stores/authStore'
import { useBookStore } from '@/stores/bookStore'

const router = useRouter()
const { authLogout } = useAuthStore()
const { user } = useBookStore()

function logout() {
  authLogout()
  router.push('/')
}
</script>

<template>
  <nav class="bg-bermuda-gray-200">
    <div class="max-w-screen-xl flex flex-wrap items-center justify-between mx-auto p-4">
      <a class="flex items-center space-x-3 rtl:space-x-reverse text-bermuda-gray-900 font-bold">
        <!-- logo -->
        Book-Club-Service
      </a>
      <button data-collapse-toggle="navbar-default" type="button"
        class="inline-flex items-center p-2 w-10 h-10 justify-center text-sm text-gray-500 rounded-lg md:hidden hover:bg-gray-100 focus:outline-none focus:ring-2 focus:ring-gray-200 dark:text-gray-400 dark:hover:bg-gray-700 dark:focus:ring-gray-600"
        aria-controls="navbar-default" aria-expanded="false">
        <span class="sr-only">Open main menu</span>
        <svg class="w-5 h-5" aria-hidden="true" xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 17 14">
          <path stroke="currentColor" stroke-linecap="round" stroke-linejoin="round" stroke-width="2"
            d="M1 1h15M1 7h15M1 13h15" />
        </svg>
      </button>
      <div class="hidden w-full md:block md:w-auto" id="navbar-default">
        <ul
          class="font-medium flex flex-col p-4 md:p-0 mt-4 border border-gray-100 rounded-lg bg-gray-50 md:flex-row md:space-x-8 rtl:space-x-reverse md:mt-0 md:border-0 md:bg-white">
          <li>
            <p class="mt-2">
              <span>
                <!--!Font Awesome Free 6.5.1 by @fontawesome - https://fontawesome.com License - https://fontawesome.com/license/free Copyright 2024 Fonticons, Inc.-->
                <svg xmlns="http://www.w3.org/2000/svg" width="30" height="30" fill="currentColor" class="ml-8"
                  viewBox="0 0 20 20">
                  <path d="M11 6a3 3 0 1 1-6 0 3 3 0 0 1 6 0z" />
                  <path fill-rule="evenodd"
                    d="M0 8a8 8 0 1 1 16 0A8 8 0 0 1 0 8zm8-7a7 7 0 0 0-5.468 11.37C3.242 11.226 4.805 10 8 10s4.757 1.225 5.468 2.37A7 7 0 0 0 8 1z" />
                </svg>
              </span>
              <span class="pl-2">{{ user?.firstname }} </span>
              <span class="pl-2">{{ user?.lastname }}</span>
            </p>
          </li>
          <li>
            <button class="text-white border rounded-xl mt-2 pt-2 bg-red-500 pl-3 pr-4 py-2"
              @click="logout">Logout</button>
          </li>
        </ul>
      </div>
    </div>
  </nav>
</template>
@/store/authStore@/stores/authStore