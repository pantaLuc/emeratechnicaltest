<template>
   <div class="hover:shadow-2xl hover:bg-transparent p-2">
     <form class="w-full max-w-lg" @submit.prevent="addTodo" >
        <div class="flex flex-wrap -mx-3 mb-6">
          <div class="w-full px-3">
            <label class="block uppercase tracking-wide text-gray-700 text-xs font-bold mb-2" for="NewTodo">
              Todo
            </label>
            <input  class="appearance-none block w-fullbg-transparent text-gray-700 border border-gray-200 rounded py-3 px-4 mb-3 leading-tight focus:outline-none focus:bg-white focus:border-gray-500" id="grid-password" type="text" placeholder="Enter a new todo" v-model="newTodo">
          </div>
        </div>
        <div class="flex flex-wrap -mx-3 mb-6">
          <div class="w-full px-3">
            <label class="block uppercase tracking-wide text-gray-700 text-xs font-bold mb-2" for="deadline">
              DeadLine
            </label>
            <input  class="appearance-none block w-full bg-transparent text-gray-700 border border-gray-200 rounded py-3 px-4 mb-3 leading-tight focus:outline-none focus:bg-white focus:border-gray-500"   type="datetime-local"    v-model="deadlineTodo">
          </div>
        </div>
      
        <div class="flex flex-wrap -mx-3 mb-6">
          <div class="w-full px-3">
            <label class="block uppercase tracking-wide text-gray-700 text-xs font-bold mb-2" for="description">
              Description 
            </label>
            <input class="appearance-none block w-full bg-transparent text-gray-700 border border-gray-200 rounded py-3 px-4 mb-3 leading-tight focus:outline-none focus:bg-white focus:border-gray-500"  type="textfield" placeholder="enter a description" v-model="descriptionTodo">
          </div>
        </div>    
      </form>
          <button class="bg-transparent hover:bg-blue-500 text-blue-700 font-semibold hover:text-white py-2 px-4 border border-blue-500 hover:border-transparent rounded w-full px-3" @click="addTodo">
           save
      </button>
      </div>
      
</template>

<script>
import { reactive, ref, toRefs } from '@vue/reactivity';
import axios from 'axios';
 
  export default {
    setup(props,ctx){
    const state=reactive({
      newTodo:" ",
      deadlineTodo:" ",
      descriptionTodo:" "
    });
    const {newTodo ,deadlineTodo,descriptionTodo}=toRefs(state)
    const addTodo=()=>{
      const data={
        "nom":newTodo.value,
        "deadline":deadlineTodo.value,
        "description":descriptionTodo.value
      };
      axios.post("http://localhost:8000/api/crud/createTask" ,data).then(setTimeout(()=>location.reload(),5));
      ctx.emit("add" ,[newTodo.value ,descriptionTodo.value,deadlineTodo.value])
      newTodo.value=" ";
      descriptionTodo.value=" ";
      deadlineTodo.value=" ";
    };
    return{
      newTodo:newTodo,
      deadlineTodo:deadlineTodo,
      descriptionTodo:descriptionTodo,
      addTodo
    }
  }
    
  }
</script>

<style>

</style>