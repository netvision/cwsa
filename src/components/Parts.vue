<template>
  <h3 class="text-h3">{{part?.partt}}</h3>
  <div v-if="part.sectors && part.sectors.length > 0">
      <Sectors v-for="(sector, i) in part.sectors" :key="i" :sector="sector" />
  </div>
  <div v-if="part.chapters && part.chapters.length > 0">
      <Chapters v-for="(chapter, i) in part.chapters" :key="i" :chapter="chapter" />
  </div>

</template>

<script setup>
import { onMounted, ref } from 'vue'
import Chapters from './Chapters.vue'
import Sectors from './Chapters.vue'
const props = defineProps({
    part: Object
  })
const part = ref({})
onMounted(()=>{
    part.value = props.part
    console.log(part)
})

</script>

<style>

</style>