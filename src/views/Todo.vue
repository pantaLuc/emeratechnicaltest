<template>

<div class="flex flex-row  ">
  <div class="grid grid-flow-row-denserow ">
    <AddTodo @add="saveTask"/>
  </div>
  <div class="container ml-10 ">
      <div class="sm:grid grid-cols-1 sm:gap-2 lg:grid-cols-3 lg:gap-3 xl:grid-cols-3 xl:gap-3">
    <display-todo />
  </div>
  </div>
</div>
  
     
   

</template>
<script>
import {ref ,reactive} from 'vue' ;
import AddTodo from './ComponentsTodo/AddTodo.vue';
import DisplayTodo from './ComponentsTodo/DisplayTodo.vue';
import axios from 'axios' ;
export default {
  
  components: { AddTodo, DisplayTodo },
  setup() {
   const saveTask=(data)=>{
    
   } 
   return{
     saveTask
   }
  }
}
</script>
