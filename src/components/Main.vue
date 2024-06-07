<script setup lang="ts">
import Pagination from './Pagination.vue'
import { getCharacters } from 'rickmortyapi'
import { watch, ref, computed } from "vue"
import ListCharacters from "./ListCharacters.vue"


const page = ref(1)

const response = ref<any>(null)
const characters = computed(() => response.value ? response.value.data.results : [])
const count_pages = computed(() => response.value ? response.value.data.info.pages : 0)
const from = computed(() => response.value ? characters.value[0].id : 0);
const to = computed(() => response.value ? characters.value[characters.value.length - 1].id : 20);
const of = computed(() => response.value ? response.value.data.info.count : 100);

const changePage = (n: number) => page.value = n

watch(page, async (new_value, old_value) => {
  response.value = await getCharacters({ page: new_value })
}, { immediate: true });

</script>

<template>
  <Pagination @change-page="changePage" :count-pages="count_pages" :current-page="page" :from="from" :to="to" :of="of">
  </Pagination>
  <ListCharacters :characters="characters"></ListCharacters>
  <pre>{{ JSON.stringify(response, null, 2) }}</pre>
</template>
