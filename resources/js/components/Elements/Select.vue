<script setup lang="ts">
import { Menu, MenuButton, MenuItem, MenuItems } from '@headlessui/vue'
import { CheckIcon, ChevronDownIcon } from '@heroicons/vue/24/solid'
import Spinner from '@/components/Elements/Spinner.vue'

interface Props {
  current?: string | number
  options: (string | number)[]
  onClick: (option: string | number) => void
  isLoading?: boolean
}

withDefaults(defineProps<Props>(), {
  isLoading: false,
})
</script>

<template>
  <Menu as="div" class="relative inline-block text-start shrink-0">
    <div class="group">
      <MenuButton
        class="inline-flex justify-center items-center w-full rounded-md shadow-sm px-4 py-2 bg-gray-100 dark:bg-gray-700 text-sm font-medium text-gray-500 dark:text-gray-300 hover:text-black dark:hover:text-white focus:outline-none focus:ring-1 focus:outline-blue-500 whitespace-no-wrap"
        :disabled="isLoading"
      >
        <Spinner class="h-4 w-4" v-if="isLoading" />
        <template v-else>
          {{ current }}
          <ChevronDownIcon
            aria-hidden="true"
            class="-me-1 ms-2 h-4 w-4 dark:group-hover:text-white group-hover:text-black"
          />
        </template>
      </MenuButton>
    </div>

    <transition
      enter-active-class="transition ease-out duration-100"
      enter-from-class="transform opacity-0 scale-95"
      enter-to-class="transform opacity-100 scale-100"
      leave-active-class="transition ease-in duration-75"
      leave-from-class="transform opacity-100 scale-100"
      leave-to-class="transform opacity-0 scale-95"
    >
      <MenuItems
        class="z-10 ltr:origin-top-left rtl:origin-top-right absolute text-xs start-0 mt-2 w-36 rounded-md shadow-lg bg-white dark:bg-gray-900 shadow-lg rounded-lg border border-gray-200 dark:border-gray-700 px-1 focus:outline-none"
        tabindex="-1"
      >
        <div class="py-1">
          <MenuItem v-for="value in options" :key="value">
            <div class="flex flex-row">
              <button
                class="flex flex-row justify-between items-center hover:bg-gray-50 dark:hover:bg-gray-800 block w-full text-start cursor-pointer py-2 px-3 focus:outline-none focus:ring-1 focus:ring-blue-500 rounded text-gray-500 dark:text-gray-500 dark:hover:text-gray-400 dark:active:text-gray-600"
                tabindex="1"
                type="button"
                @click.prevent="onClick(value)"
              >
                <span class="truncate">{{ value }}</span>
                <span v-if="current === value">
                  <CheckIcon aria-hidden="true" class="h-4 w-4 text-blue-500" />
                </span>
              </button>
            </div>
          </MenuItem>
        </div>
      </MenuItems>
    </transition>
  </Menu>
</template>
