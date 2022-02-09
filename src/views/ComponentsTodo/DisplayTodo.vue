<template>
     
   
      
          <div class="max-w-xs h-40 flex flex-col justify-between bg-white dark:bg-gray-800 rounded-lg border border-white-400 mb-2 py-2 px-2 hover:shadow-2xl"  v-for="todo  in todos" :key="todo.id" v-show="todos" >
              <div>
                  <div class="inline-flex items-baseline">
                   
                     <h3   class="text-indigo-400 hover:text-indigo-500 font-bold mb-3 " >{{todo.nom}} </h3> 
                     <button class="px-2 ml-8 inline-flex text-xs leading-5 font-semibold rounded-full bg-green-300 text-white" @click="changeStatus(todo)"> {{todo.status}} </button>
                  </div>
                  <h4 class="text-gray-800 dark:text-gray-100 text-sm">{{todo.description}}</h4>
              </div>
              <div>
                  <div class="flex items-center justify-between text-gray-800">
                      <p class="text-sm dark:text-gray-150 font-semibold">{{ modifDate(todo.deadline)}}</p>
                       
                      <button class="text-red-800  hover:text-indigo-500 "  @click="deleteTodo(todo)"><i class="fas fa-trash-alt text-red"></i></button>
                  </div>
              </div>
          </div> 
     
  

</template>
<script>
import axios from 'axios';
import moment from 'moment';
import { computed, ref } from '@vue/reactivity';
import { watch } from '@vue/runtime-core'
export default {
 /*data() {
   return {
     todos:ref(null)
   }
 },
 mounted() {
   axios.get('http://127.0.0.1:8000/api/crud/listTask/').then(
        response=>(this.todos=response.data)
      )
 },*/
 setup(props ,ctx){
   const todos=ref([])
   const updateTodo=(todo)=>{
      ctx.emit("update",todo)
   };
   const deleteTodo=(todo)=>{
      axios.delete(`http://localhost:8000/api/crud/task/${todo.id}`).then(setTimeout(()=>{location.reload()},10))
    
   };
   
     axios.get('http://127.0.0.1:8000/api/crud/listTask/').then(
        response=>(todos.value=response.data)
      )
      
  const modifDate =function (date ) {
     
    return moment(date).format('llll');
  }
  const changeStatus=(todo)=>{
    todo.status=="ongoing"?  axios.put(`http://localhost:8000/api/crud/task/${todo.id}` , {"status":"done"}).then(setTimeout(()=>{location.reload()} ,5)): axios.put(`http://localhost:8000/api/crud/task/${todo.id}` , {"status":"ongoing"}).then(setTimeout(()=>{location.reload()} ,5))
   
  }
   return{
    changeStatus,
    modifDate,
     todos,
     updateTodo,
     deleteTodo
   }
 }
 
}

</script>

<style scoped>
body {
    font-family: "Lato", sans-serif;
};



</style>

