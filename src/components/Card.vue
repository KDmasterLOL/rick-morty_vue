<script setup lang="ts">
import { computed, onMounted } from 'vue'
const props = defineProps<{
  imageUrl: string
  name: string
  origin: string
  location: string
  status: string
  species: string

}>()

const back = computed(() => {
  switch (props.status) {
    case 'Alive': return "bg-green-600"
    case 'unknown': return "bg-gray-500"
    case 'Dead': return "bg-red-600"
  }
}
)

</script>

<template>
  <section
    class="flex  bg-white h-min rounded-md overflow-hidden shadow  dark:bg-gray-800 dark:border-gray-700 dark:hover:bg-gray-700">
    <img class="h-100" :src="imageUrl" alt="">
    <div class="p-2">
      <h5 class="mb-2 text-2xl font-bold tracking-tight text-gray-900 dark:text-white">{{ name }}</h5>
      <p class="font-normal text-sm text-gray-700 dark:text-gray-200">
        <span class="w-2.5 h-2.5 inline-block rounded-full" :class="back"> </span>
        {{ status }} - {{ species }}
      </p>
      <p class="font-normal text-sm text-gray-400 dark:text-gray-400">Last known location:</p>
      <p class="font-normal text-gray-700 hover:text-orange-400 dark:text-gray-200">{{ location }}</p>
      <p class="font-normal text-sm text-gray-400 dark:text-gray-400">First seen in:</p>
      <p class="font-normal text-gray-700 hover:text-orange-400 dark:text-gray-200">{{ origin }}</p>
    </div>
  </section>
</template>
