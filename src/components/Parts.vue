<template>
  <h3 class="text-h3">{{part?.partt}}</h3>
  <div v-if="part.sections && part.sections.length > 0">
      <Sections v-for="(sect, i) in part.sections" :key="i" :section="sect" />
  </div>
  <div v-if="part.chapters && part.chapters.length > 0">
      <Chapters v-for="(chapter, i) in part.chapters" :key="i" :chapter="chapter" />
  </div>

</template>

<script setup>
import { onMounted, ref } from 'vue'
import Chapters from './Chapters.vue'
import Sections from './Sections.vue'
const props = defineProps({
    part: Object
  })
const part = ref({})
onMounted(()=>{
    part.value = props.part
})

</script>

<style>

</style>