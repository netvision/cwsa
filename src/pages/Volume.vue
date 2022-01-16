<template>
    <q-page class="q-pa-md" v-if="volume.length > 0">
        <div v-for="vol in volume" :key="vol._id">
            <h2 class="text-h2">{{vol.t}}</h2>
            <div v-if="vol.toc.books && vol.toc.books.length > 0">
                <Books v-for="(book, i) in vol.toc.books" :key="i" :book = "book" />
            </div>
            <div v-if="vol.toc.parts && vol.toc.parts.length > 0">
                <Parts v-for="(part, i) in vol.toc.parts" :key="i" :part = "part" />
            </div>
        </div>
    </q-page>
</template>

<script setup>
import { onMounted, ref } from 'vue'
import { useRoute } from 'vue-router'
import Parts from '../components/Parts.vue'
import Books from '../components/Books.vue'
const route = useRoute()
const vol = route.params.vol 
const volume = ref([])

onMounted(()=>{
    volume.value = require('../data/cwsa_'+vol+'_index.json')
    console.log(volume.value)
})

</script>

<style>

</style>