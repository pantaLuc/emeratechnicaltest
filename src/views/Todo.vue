<template>
<div class="flex md:flex-row-reverse flex-wrap">
  <div class="w-full md:w-3/4 p-4 text-gray-200">
   
  <display-todo/>
  
  </div>
  <div class="w-full md:w-1/4  text-gray-700">
  
    <add-todo/>
  </div>
</div>
</template>
<script>
import {ref ,reactive} from 'vue' ;
import AddTodo from './ComponentsTodo/AddTodo.vue';
import DisplayTodo from './ComponentsTodo/DisplayTodo.vue';

export default {
  components: { AddTodo, DisplayTodo },
  
}
</script>
