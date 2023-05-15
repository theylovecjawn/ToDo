<script setup>
  import {ref, watch} from 'vue'

  let todos = ref(JSON.parse(window.localStorage.getItem('todos')))



  watch(todos, function(value){
    window.localStorage.setItem('todos', JSON.stringify(value))
  }, {deep: true})
  
  let newTodo = ref("")


  function popUpTodo(){
    todos.value.push({
      text: newTodo.value,
      complete:false
      })
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
  {{ todo.text }}
  <label class="container"><input type="checkbox" v-model="todo.complete"><span class="checkmark"></span></label>
  </li>
</ol>
<p><input v-model="newTodo" @keydown.enter="popUpTodo" id="inputBox" placeholder="Click Me to Start"></p>
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
  background-color: transparent;
  border-radius: 8px;

}
/* Customize the label (the container) */
.container {
  margin: 20px;
  position: relative;
  padding-left: 35px;
  margin-bottom: 15px;
  cursor: pointer;
  font-size: 22px;
  -webkit-user-select: none;
  -moz-user-select: none;
  -ms-user-select: none;
  user-select: none;
}

/* Hide the browser's default checkbox */
.container input {
  position: absolute;
  opacity: 0;
  cursor: pointer;
  height: 0;
  width: 0;
}

/* Create a custom checkbox */
.checkmark {
  position: absolute;
  top: 0;
  left: 0;
  height: 25px;
  width: 25px;
  background-color: #eee;
}

/* On mouse-over, add a grey background color */
.container:hover input ~ .checkmark {
  background-color: #ccc;
}

/* When the checkbox is checked, add a blue background */
.container input:checked ~ .checkmark {
  background-color: #2196F3;
}

/* Create the checkmark/indicator (hidden when not checked) */
.checkmark:after {
  content: "";
  position: absolute;
  display: none;
}

/* Show the checkmark when checked */
.container input:checked ~ .checkmark:after {
  display: block;
}

/* Style the checkmark/indicator */
.container .checkmark:after {
  left: 9px;
  top: 5px;
  width: 5px;
  height: 10px;
  border: solid white;
  border-width: 0 3px 3px 0;
  -webkit-transform: rotate(45deg);
  -ms-transform: rotate(45deg);
  transform: rotate(45deg);
}


</style>
