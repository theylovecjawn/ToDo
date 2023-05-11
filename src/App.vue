<script setup>
  import {ref} from 'vue'

  let todos = ref([])
  let newTodo = ref("")

  function popUpTodo(){
    todos.value.push(newTodo.value)
    newTodo.value = ""
  }
  function deleteTodo(index){
    todos.value.splice(index, 1)  
  }
</script>

<template>
  <h1>My Todo List</h1>
  <ol>
  <li v-for="(todo, index) in todos">
    <button id="icon" @click="deleteTodo(index)">🗑</button>
  {{ todo }}
  </li>
</ol>
<p><input v-model="newTodo" @keydown.enter="popUpTodo" id="inputBox"></p>
<p><button @click="popUpTodo" id="submitThing">Add Todo</button></p>
</template>

<style>
body{
  background-color: paleturquoise;
}
h1{
  text-align: center;

}
li{
  list-style-position: inside;
  text-align: center;
}
#submitThing{
align-items: center;
}
p{
  text-align: center;
}
#icon{
  background-color: transparent;
  border: none;

}
#icon:hover{
  background-color: brown;
}
#submitThing{
  margin: 5px 3px 10px 5px;
    padding: 5px 10px;
    border-radius: 7px;
    background-color: #90EE90;
    border-style: none;
    font-size: 20px;
    top: 150px;
    position: relative;
}
#submitThing:hover{
  background-color:beige;
}
#inputBox{
  top: 145px;
    position: relative;
}

</style>
