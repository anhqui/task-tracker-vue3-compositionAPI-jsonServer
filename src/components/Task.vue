<template>
<div 
@dblclick="onToggle" 
:class="[task.reminder ? 'reminder' : '', 'task']">
<h3>
    {{task.text}}
    <i @click="onDelete" class="fas fa-times"></i>
    </h3>
  <p>{{task.day}}</p>
</div>
</template>

<script setup>
import {defineProps} from 'vue'

const props = defineProps({
    task:{
        type: Object,
        required: true
    }
})

const emit = defineEmits(['delete-task','toggle-reminder'])

const onDelete = (id) => {
    emit('delete-task', id);
}

const onToggle = (id) =>{
    emit('toggle-reminder', id);
}

</script>

<style scoped>
.fas::before{
    font-family: fontAwesome;
}
.fas{
    color: red;
}
.task{
    background-color: #f4f4f4;
    margin: 5px;
    padding: 10px 20px;
    cursor: pointer
}

.task.reminder{
    border-left: 5px solid green;
}

.task h3{
    display: flex;
    align-items: center;
    justify-content: space-between;
}
</style>