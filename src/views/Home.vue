<template>
<AddTask v-show="showAddTask" @add-task="addTask" />
<Tasks 
@toggle-reminder="toggleReminder" 
@delete-task="deleteTask" :tasks="tasks" />
</template>

<script setup>
import Tasks from '../components/Tasks.vue'
import AddTask from '../components/AddTask.vue'

import {ref} from "vue"

import {defineProps} from 'vue'

const props = defineProps({
    showAddTask:{
        type: Boolean,
        required: true
    }
})


 const tasks = ref([])
 


const fetchTasks = async () => {
  const res = await fetch('http://localhost:5000/tasks')
  const data = await res.json()
  // console.log(data)
  tasks.value = await data;

}

fetchTasks()

const fetchTask = async (id) => {
  const res = await fetch(`http://localhost:5000/tasks/${id}`)
  const data = await res.json()
  return data

}

const deleteTask = async (id) =>{
  // console.log('task',id)
  if(confirm('Are you sure?')){
    const res = await fetch(`http://localhost:5000/tasks/${id}`, {
      method: 'DELETE'
    })
res.status === 200 ? (tasks.value = tasks.value.filter(task => task.id !== id)) : alert('Error deleting task')
    // tasks.value = tasks.value.filter(task => task.id !== id)
  }
}

const toggleReminder = async (id) =>{
  // console.log(id)
  const taskToToggle = await fetchTask(id)
  const updTask = {...taskToToggle, reminder: !taskToToggle.reminder}

  const res = await fetch(`http://localhost:5000/tasks/${id}`,{
    method: 'PUT',
    headers:{
      'Content-type': 'application/json'
    },
    body: JSON.stringify(updTask)
  })

  const data = await res.json()

  tasks.value = tasks.value.map(task => task.id === id ? {...task, reminder: data.reminder} : task)
}

const addTask = async (newTask) =>{
  const res = await fetch('http://localhost:5000/tasks', {
    method: 'POST',
    headers: {
      'Content-type': 'application/json',
    },
     body: JSON.stringify(newTask)
  })
  
  const data = await res.json()

  tasks.value.push({
    id: generateUniqueId(),
    text: data.text,
    day: data.day,
    reminder: data.reminder
  })

}
const generateUniqueId = () =>{
  return  Math.floor(Math.random() * 100000)
}




</script>
