<template>
<div v-for="task in tasks" :key="task.id">
<Task 
@toggle-reminder="$emit('toggle-reminder', task.id)" 
@delete-task="$emit('delete-task', task.id)" :task="task" />
</div>

</template>

<script setup>
import {defineProps} from 'vue';
import Task from './Task.vue'

const emit = defineEmits(['delete-task','toggle-reminder'])

const props = defineProps({
    tasks: {
        type: Array,
        required: true
    }
})

</script>

