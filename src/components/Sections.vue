<template>
  <h3 class="text-h3">{{section?.sect}}</h3>
  <div v-if="sector.chapters && sector.chapters.length > 0">
      <Chapters v-for="(chapter, i) in sector.chapters" :key="i" :chapter="chapter" />
  </div>
</template>

<script setup>
import { onMounted, ref } from 'vue'
import Chpater from './Chapters.vue'
const props = defineProps({
    sector: Object
  })
const sector = ref({})
onMounted(()=>{
    sector.value = props.sector
    console.log(sector)
})

</script>

<style>

</style>