<script setup lang="ts">
import { MagnifyingGlassIcon } from '@heroicons/vue/24/outline'
import debounce from 'lodash/debounce'
import { computed } from 'vue'
import useBrowserStore from '@/stores/browser'

const store = useBrowserStore()

// STATE
const search = computed(() => store.search)

const setSearch = debounce(({ target: { value } }) => {
  store.setSearch({ search: value })
}, window.Nova.config('debounce'))
</script>

<template>
  <div class="relative rounded-md w-full md:w-64 md:focus-within:w-full md:duration-500 md:transition-all">
    <div class="absolute inset-y-0 start-0 ps-3 flex items-center pointer-events-none">
      <MagnifyingGlassIcon aria-hidden="true" class="h-4 w-4 text-gray-400" />
    </div>
    <input
      :placeholder="__('Search')"
      :value="search"
      class="rounded-full pe-3 h-9 ps-8 w-full bg-gray-100 focus:dark:bg-gray-700 dark:bg-gray-700/40 dark:focus:bg-gray-800 focus:bg-white focus:outline-none focus:ring-1 focus:outline-blue-500 text-sm placeholder-gray-500 text-gray-500 dark:text-gray-200"
      type="search"
      @input="setSearch"
    />
  </div>
</template>
