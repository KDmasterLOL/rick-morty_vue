<script setup lang="ts">
import Pagination from './Pagination.vue'
import { getCharacters } from 'rickmortyapi'
import { watch, watchEffect, ref, computed } from "vue"
import ListCharacters from "./ListCharacters.vue"


const page = ref(1)

const response = ref<any>(null)
const characters = ref<any>([])
const count_pages = ref<any>(0)
const from = ref<any>(0)
const to = ref<any>(0)
const of = ref<any>(0)
const filter_status = ref("")
const filter_name = ref("")
const changePage = (n: number) => page.value = n

watchEffect(async () => {
  getCharacters({ page: page.value, name: filter_name.value, status: filter_status.value })
    .then((v) => {
      response.value = v
      characters.value = response.value.data.results
      count_pages.value = response.value.data.info.pages
      from.value = (page.value - 1) * 20
      to.value = from.value + characters.value.length
      of.value = response.value.data.info.count
    }).catch(v => {
    })
})

</script>

<template>
  <Pagination @change-page="changePage" :count-pages="count_pages" :current-page="page" :from="from" :to="to" :of="of">
  </Pagination>
  <div class="flex justify-center mt-4">
    <span class="mr-4">Status: </span>
    <select name="" id="" class="text-black" v-model="filter_status">
      <option value="">Empty</option>
      <option value="alive">Alive</option>
      <option value="dead">Dead</option>
      <option value="undefined">Undefined</option>
    </select>
    <span class="ml-8 mr-4">Name: </span>
    <input type="text" v-model="filter_name" class="text-black">
  </div>
  <ListCharacters :characters="characters"></ListCharacters>
</template>
