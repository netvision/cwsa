<template>
  <h6 class="text-h6" @click="goTo(chapter.u)">{{chapter.chapt}}</h6>
  
</template>

<script setup>
import { onMounted, ref } from 'vue'
import { useRouter, useRoute } from 'vue-router'
const props = defineProps({
    chapter: Object
  })

const router = useRouter()
const route = useRoute()
const chapter = ref({})
const vol = route.fullPath.split("/").at(-1)
const goTo = (u) =>{
    router.push('/read/'+vol+'_'+u)
}
onMounted(()=>{
    chapter.value = props.chapter
    
})

</script>

<style>

</style>