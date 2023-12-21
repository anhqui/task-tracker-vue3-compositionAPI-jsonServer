<template>
  <header>
    <h1>{{title}}</h1>
    <Button 
    v-show="homePage()"
    @btn-click="$emit('toggle-add-task')" 
    class="btn" 
    :text="showAddTask ? 'Close': 'Add Task'" 
    :color="showAddTask ? 'red' : 'green'"
    />
  </header>
</template>

<script setup>
import { defineProps} from 'vue';
import Button from './Button.vue';
import {ref} from 'vue'
import {  useRoute } from 'vue-router'

 const route = useRoute()

const props = defineProps({
    title:{
        type: String,
        required: true,
        default: "Add item"
    },
    showAddTask:{
      type: Boolean,
      required: true
    }
})


const homePage = () => {
  if(route.path === '/'){
    return true
  }else{
    return false
  }
}

</script>

<style scoped>
header{
    display: flex;
    justify-content: space-between;
    align-items: center;
    margin-bottom: 20px;
}
</style>