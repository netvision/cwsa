<template>
  <h3 class="text-h3">{{section?.sect}}</h3>
  <div v-if="section.chapters && section.chapters.length > 0">
      <Chapters v-for="(chapter, i) in section.chapters" :key="i" :chapter="chapter" />
  </div>
</template>

<script setup>
import { onMounted, ref } from 'vue'
import Chapters from './Chapters.vue'
const props = defineProps({
    section: Object
  })
const section = ref({})
onMounted(()=>{
    section.value = props.section
})

</script>

<style>

</style>