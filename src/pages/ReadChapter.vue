<template>
    <h2>{{chapt?.t}}</h2>
    <div class="q-pa-md" v-if="chapt.desc">
        <Markdown :source="chapt.desc" breaks typographer />
    </div>
    <div class="q-pa-md" v-if="chapt.txt">
        <Markdown :source="chapt.txt" html breaks typographer :plugins="plugins" />
    </div>
    <div v-if="chapt.items && chapt.items.legth > 0">
        <div v-for="(it, i) in chapt.items" :key="i">
            {{it.t}}
        </div>
    </div>
    <pre>{{chapt.items}}</pre>
</template>
<script setup>
import { useRoute } from 'vue-router'
import { ref, onMounted } from 'vue'
import Markdown from 'vue3-markdown-it'
import MarkdownItFootnote from 'markdown-it-footnote'
import Items from '../components/Items.vue'
const route = useRoute()

const v = route.params.u.split('_').at(0)
const u = route.params.u.split('_').at(-1)

const chapt = ref({})
const plugins = [
        {
          plugin: MarkdownItFootnote
        }
      ]
onMounted(()=>{
    let volume = require('../data/cwsa_'+v+'.json')
    let chapters = volume.filter(vol => vol._slugs[0] == u)
    chapt.value = (chapters && chapters.length > 0) ? chapters[0] : {}
    console.log(chapt.value)
})

</script>