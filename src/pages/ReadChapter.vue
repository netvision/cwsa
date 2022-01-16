<template>
    <h2>{{chapt?.t}}</h2>
    <div class="q-pa-md" v-if="chapt.desc">
        <Markdown :source="chapt.desc" breaks typographer />
    </div>
    <div class="q-pa-md" v-if="chapt.txt" v-html="htmlText">
        
    </div>
    <div v-if="chapt.items && chapt.items.length > 0">
       <Items v-for="(it, i) in chapt.items" :key="i" :item="it" />
    </div>
</template>
<script setup>
import { useRoute } from 'vue-router'
import { ref, onMounted } from 'vue'
import Markdown from 'vue3-markdown-it'
import MarkdownItFootnote from 'markdown-it-footnote'
import showdown from 'showdown'
import footnotes from 'showdown-footnotes'
import Items from '../components/Items.vue'
const route = useRoute()

const v = route.params.u.split('_').at(0)
const u = route.params.u.split('_').at(-1)
const converter = new showdown.Converter({ extensions: [footnotes] })
const chapt = ref({})
const plugins = [
        {
          plugin: MarkdownItFootnote
        }
      ]
const htmlText = ref('')
const sanitizeHtml = (html) => {
  let placeholder = document.createElement('div')
  placeholder.innerHTML = html
  placeholder.querySelectorAll('em').forEach(
    (el) => {
      el.style = "color: blue; font-weight: bold; font-size:16px"
    }
  )
  placeholder.querySelectorAll('span.page-number').forEach(
      (el) => {
          el.innerHTML = ''
      }
  )
  return placeholder.innerHTML
}
onMounted(()=>{
    let volume = require('../data/cwsa_'+v+'.json')
    let chapters = volume.filter(vol => vol._slugs[0] == u)
    
    chapt.value = (chapters && chapters.length > 0) ? chapters[0] : {}
    console.log(chapt.value.items)
    htmlText.value = sanitizeHtml(converter.makeHtml(chapt.value.txt))
})

</script>