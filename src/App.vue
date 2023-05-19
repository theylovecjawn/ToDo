<script setup>
  import {ref, watch} from 'vue'
  let filter = ref('all')

  let todos = ref(JSON.parse(window.localStorage.getItem('todos')) ??[])



  watch(todos, function(value){
    window.localStorage.setItem('todos', JSON.stringify(value))
  }, {deep: true})

  function activeFilter(todo){
    return todo.complete == false
  }
  
  function todoFilter(todo){
    if (filter.value == "active"){
      return todo.complete == false
    }
    else if (filter.value == 'complete') {
      return todo.complete == true
      
    }
    else {
      return true
    }
  }


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


  <ul id="scroll">
  <li v-for="(todo, index) in todos.filter(todoFilter)" >
    <label class="container"><input type="checkbox" v-model="todo.complete"><span class="checkmark"></span></label>
  <span :class="{completed: todo.complete}">{{ todo.text }}</span>
  <button class="icon" @click="deleteTodo(index)">❌</button>
  <hr>
  
  
  </li>
</ul>
<p v-if="todos.length > 0">

  <p>{{todos.filter(activeFilter).length}} items left</p>
<label class="form-control"><input name="filter" type="radio" value="all" v-model="filter"></label>
  <label class="bigger">All      </label>

  <label class="form-control"><input name="filter" type="radio" value="active" v-model="filter"></label>
  <label class="bigger">Active      </label>

  <label class="form-control"><input name="filter" type="radio" value="complete" v-model="filter"></label>
  <label class="bigger">Completed      </label>
</p>        

<p><input v-model="newTodo" @keydown.enter="popUpTodo" id="inputBox" placeholder="Click Me to Start"></p>
<p><button @click="popUpTodo" id="submitThing">Add Todo</button></p>
</template>

<style>
@import url('https://fonts.googleapis.com/css2?family=Rajdhani:wght@300&family=Shadows+Into+Light&family=Smokum&display=swap');
body{
  font-family: 'Rajdhani', sans-serif;
font-family: 'Shadows Into Light', cursive;
font-family: 'Smokum', cursive;
  background-color: black;
  color: aliceblue;
  
}
h1{
  text-decoration: underline;
  text-align: center;
  color: white;

}
.form-control {
  font-family: system-ui, sans-serif;
  font-size: 2rem;
  font-weight: bold;
  line-height: 1.1;
  display: grid;
  grid-template-columns: 1em auto;
  gap: 0.5em;
}






:root {
  --form-control-color: rgb(146, 202, 221);
}

*,
*:before,
*:after {
  box-sizing: border-box;
}

body {
  margin: 0;
}

form {
  display: grid;
  place-content: center;
  min-height: 100vh;
}

.form-control {
  font-family: system-ui, sans-serif;
  font-size: 2rem;
  font-weight: bold;
  line-height: 1.1;
  display: inline-grid;
  grid-template-columns: 1em auto;
  gap: 0.5em;
}

.form-control + .form-control {
  margin-top: 1em;
}

.form-control:focus-within {
  color: var(--form-control-color);
}

input[type="radio"] {
  /* Add if not using autoprefixer */
  -webkit-appearance: none;
  /* Remove most all native input styles */
  appearance: none;
  /* For iOS < 15 */
  background-color: var(--form-background);
  /* Not removed via appearance */
  margin: 0;

  font: inherit;
  color: currentColor;
  width: 1.15em;
  height: 1.15em;
  border: 0.15em solid currentColor;
  border-radius: 50%;
  transform: translateY(-0.075em);

  display: grid;
  place-content: center;
}

input[type="radio"]::before {
  content: "";
  width: 0.65em;
  height: 0.65em;
  border-radius: 50%;
  transform: scale(0);
  transition: 120ms transform ease-in-out;
  box-shadow: inset 1em 1em var(--form-control-color);
  /* Windows High Contrast Mode */
  background-color: CanvasText;
}

input[type="radio"]:checked::before {
  transform: scale(1);
}

input[type="radio"]:focus {
  outline: max(2px, 0.15em) solid currentColor;
  outline-offset: max(2px, 0.15em);
}












li{
  list-style-position: inside;
  margin: 0 auto;
  max-width: 500px;
}

p{
  text-align: center;
}
.icon{
  background-color: transparent;
  border: none;
  float: right;
  display: none;

}
.icon:hover{
  background-color: rgb(198, 179, 179);
}

li:hover > .icon{
  display: inline;
}
#submitThing{
  
    padding: 5px 10px;
    border-radius: 7px;
    background-color: rgb(146, 202, 221);
    border-style: none;
    font-size: 20px;
    top: 700px;
    position: static;
}
#submitThing:hover{
  background-color:beige;
}
#inputBox{
  top: 750px;
  position: static;
  background-color: transparent;
  border-radius: 8px;
  color: white;
  

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
  background-color: #aaa;
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
.completed{
  color: #ccc;
  text-decoration: line-through;
  text-decoration-color: black;
}
#scroll{
  background-color: rgb(146, 202, 221);
  border-radius: 1111px;
  margin: auto;
  max-height: 442px;
  overflow-y: scroll;
}
.bigger{
  font-size: 30px;
}






</style>
