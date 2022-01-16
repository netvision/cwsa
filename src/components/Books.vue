<template>
<h4 class="text-h4">{{book.bookt}}</h4>
<div v-if="book.parts && book.parts.length > 0">
    <Parts v-for="(part, i) in book.parts" :key="i" :part = "part" />
</div>
</template>

<script setup>
import { onMounted, ref } from 'vue'
import Parts from './Parts.vue'
const props = defineProps({
    book: Object
  })
const book= ref({})
onMounted(()=>{
    book.value = props.book
    console.log(book)
})

</script>

<style>

</style>