<template>
   <button :style="{background: color}" class="btn" @click="onClick">{{text}}</button>
</template>

<script setup>
import {defineProps} from "vue";

const props = defineProps({
    text:{
        type: String,
        required: true
    },
    color:{
        type: String,
        required: true
    }
})

const emit = defineEmits(['btn-click'])

const onClick = ()=>{
    // console.log("click")
    emit('btn-click')
}

</script>

<style scoped>

</style>