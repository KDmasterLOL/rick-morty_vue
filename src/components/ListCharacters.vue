<script setup lang="ts">
import Card from './Card.vue'

const props = defineProps<{
  characters: any[]
}>()
</script>

<template>
  <div class="m-auto w-fit grid grid-cols-1 lg:grid-cols-2 gap-2 p-4 ">
    <Card v-for="p in characters" :image-url="p.image" :name="p.name" :origin="p.origin.name"
      :location="p.location.name" :status="p.status" :species="p.species"></Card>
  </div>
</template>
