<template>
    <h3>Items</h3>
    {{item}}
</template>
<script setup>
import { onMounted, ref } from 'vue'
const props = defineProps({
    item: Object
})

const item = ref(props.item)
</script>