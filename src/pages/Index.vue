<template>
  <q-page class="flex flex-center">
    <div class="q-pa-md">
      <h2 class="text-h2">{{cwsa.cmpn}}</h2>
      <Markdown :source="cwsa.desc" breaks typographer />
    </div>
   <div class="q-pa-md" v-for="vol in cwsa.vols" :key="vol.url">
      <q-list>
        <q-item v-for="(vol) in cwsa.vols" :key="vol.url">
          <q-item-section @click="goToVol(vol.vol)">
            <q-item-label class="text-h4">{{vol.t}}</q-item-label>
            <q-item-label><Markdown :source="vol.desc" breaks typographer /></q-item-label>
          </q-item-section>
        </q-item>
      </q-list>
   </div>
  </q-page>
</template>

<script setup>
import { ref, onMounted } from 'vue'
import { useRouter } from 'vue-router'
//import Nl2br from 'vue3-nl2br'
import 'highlight.js/styles/monokai.css';
import Markdown from 'vue3-markdown-it';
const router = useRouter()
const cwsa = ref({})

const goToVol = (vol) => {
  router.push('/volume/'+vol)
}



onMounted(() => {
  cwsa.value = require('../data/cwsa.json')
  console.log(cwsa.value)

  document.addEventListener('mouseup', event => {
        const selection = window.getSelection()
        console.log(selection.toString())
      
  })
})

</script>
