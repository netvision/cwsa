<template>
    <h3>{{item.t}}</h3>
</template>
<script setup>
import { onMounted, ref } from 'vue'
const props = defineProps({
    item: Object
})

const item = ref(props.item)
</script>