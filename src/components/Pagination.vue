<script setup lang="ts">
const props = defineProps<{
  countPages: number
  currentPage: number
  from: number
  to: number
  of: number
}>();
const emit = defineEmits<{
  changePage: [next_page: number]
}>()

</script>
<template>
  <section class="flex items-center justify-between border-t border-gray-200 bg-white px-4 py-3 sm:px-6">
    <p class="text-sm text-gray-700">
      Showing
      <span class="font-medium">{{ from }}</span>
      to
      <span class="font-medium">{{ to }}</span>
      of
      <span class="font-medium">{{ of }}</span>
      results
    </p>
    <nav class="flex max-w-[60%] rounded-md shadow-sm" aria-label="Pagination">
      <a href="#" @click="emit('changePage', currentPage - 1)"
        class="inline-flex items-center rounded-l-md px-2 py-2 text-gray-400 ring-1 ring-inset ring-gray-300 hover:bg-gray-50 focus:z-20 focus:outline-offset-0">
        &lt;-
      </a>
      <div class="overflow-x-scroll">
        <div class="w-max h-full">
          <a href="#" aria-current="page" v-for="n of countPages" @click="emit('changePage', n)"
            class="inline-flex items-center h-full px-4 py-2 text-sm font-semibold ring-1 ring-inset ring-gray-300"
            :class="n == currentPage ? 'text-white bg-indigo-600' : 'text-black'">{{
              n
            }}</a>
        </div>
      </div>
      <a href="#" @click="emit('changePage', currentPage + 1)"
        class="flex text-nowrap items-center rounded-r-md px-2 py-2 text-gray-400 ring-1 ring-inset ring-gray-300 hover:bg-gray-50 focus:z-20 focus:outline-offset-0">
        -&gt;
      </a>
    </nav>
  </section>
</template>
