<script setup>
import {ref, watch} from 'vue'
let filter = ref('all')
let todos = ref(JSON.parse(window.localStorage.getItem('todos')))
let touch = ref('')

function uno(){
  todos.value.push({
  text: touch.value,
  complete: false
})

touch.value = ''

}

function deleteLast () {
  if(touch.value == "") {
    todos.value.pop()
  }
 
}

function dos(){
  todos.value = []
}

function deleteI (index) {
  todos.value.splice(index, 1)

}

watch(todos, function(value) {
  window.localStorage.setItem('todos', JSON.stringify(value))
}, {deep: true})


function todoFilter (todo) {
if (filter.value == 'active') {
return todo.complete == false
} else if (filter.value == 'complete') {
return todo.complete == true
} else {
  return true
}
}


function activeFilter (todo) {
  return todo.complete == false
}


</script>




<template>
<h1>My Todo Application</h1>

<div class="todo-app">

<p>You have {{todos.filter(activeFilter).length}} items left</p>

<hr>


<p v-if="todos.length > 0">
<input name="filter" type="radio"  value="all" v-model="filter">
<label>All</label>


<input name="filter" type="radio"  value="active" v-model="filter">
<label>Active</label>


<input name="filter" type="radio"  value="complete" v-model="filter">
<label>Complete</label>
</p>

<hr>


<li v-for="(todo, index) in todos.filter(todoFilter)" :class="{completed: todo.complete}" class="myDIV">
  <label class="container"><input type="checkbox" v-model="todo.complete"><span class="checkmark"></span></label>
  <button @click="deleteI(index)" class="hide">🗑</button>
  {{todo.text}}
</li>
<input v-model="touch" @keydown.enter="uno" @keydown.delete="deleteLast">
<button @click="uno">Add Todo</button>
<button @click="dos">Clear</button>

</div>

</template>

<style>

.hide {
  display: none;
}

.myDIV:hover > .hide {
  display: inline-block;
  color: green;
}





.todo-app {
  width: 100%;
  max-width: 540px;
  background-color: #d72d7c;
  margin: 0% auto 20px;
  padding: 40px 30px 70px;
  border-radius: 10px;
  box-shadow: 20px 20px 20px 20px #000000;



}



body {
  font-weight: bold;
    font-size: large;
color: #fefefe;
background-color: #03FF41;
background-image: url("data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' width='100%25' height='100%25' viewBox='0 0 1600 800'%3E%3Cg stroke='%2352FFEA' stroke-width='100' stroke-opacity='0' %3E%3Ccircle fill='%2303FF41' cx='0' cy='0' r='1800'/%3E%3Ccircle fill='%236df500' cx='0' cy='0' r='1700'/%3E%3Ccircle fill='%2398ea00' cx='0' cy='0' r='1600'/%3E%3Ccircle fill='%23badd00' cx='0' cy='0' r='1500'/%3E%3Ccircle fill='%23d7cf00' cx='0' cy='0' r='1400'/%3E%3Ccircle fill='%23f1bf00' cx='0' cy='0' r='1300'/%3E%3Ccircle fill='%23ffad00' cx='0' cy='0' r='1200'/%3E%3Ccircle fill='%23ff9800' cx='0' cy='0' r='1100'/%3E%3Ccircle fill='%23ff8100' cx='0' cy='0' r='1000'/%3E%3Ccircle fill='%23ff6500' cx='0' cy='0' r='900'/%3E%3Ccircle fill='%23ff4131' cx='0' cy='0' r='800'/%3E%3Ccircle fill='%23ff0051' cx='0' cy='0' r='700'/%3E%3Ccircle fill='%23ff006e' cx='0' cy='0' r='600'/%3E%3Ccircle fill='%23ff008b' cx='0' cy='0' r='500'/%3E%3Ccircle fill='%23ff00a9' cx='0' cy='0' r='400'/%3E%3Ccircle fill='%23ff00c7' cx='0' cy='0' r='300'/%3E%3Ccircle fill='%23ff00e4' cx='0' cy='0' r='200'/%3E%3Ccircle fill='%23F500FF' cx='0' cy='0' r='100'/%3E%3C/g%3E%3C/svg%3E");
background-attachment: fixed;
background-size: cover;
font-family: 'Gill Sans', 'Gill Sans MT', Calibri, 'Trebuchet MS', sans-serif;
text-align: center;
}

button:hover{
background-color: rgb(0, 0, 0);
}

button {
    color: rgb(255, 255, 255);
    background-color: rgb(251, 97, 1);
    font-size: 85%;
    font-weight: bold;
    border-radius: 15%;
    border-color: rgb(0, 0, 0);
    border-width: 7px;
    }

    .completed {
      background-color: rgb(78, 81, 77);
      text-decoration: line-through;


}


/* Customize the label (the container) */
.container {
  position: relative;
  padding-left: 35px;
  margin-bottom: 12px;
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
  background-color: rgb(255, 255, 255);
}

/* On mouse-over, add a grey background color */
.container:hover input ~ .checkmark {
  background-color: rgb(0, 0, 0);
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
  height: 7px;
  border: solid white;
  border-width: 0 3px 3px 0;
  -webkit-transform: rotate(45deg);
  -ms-transform: rotate(45deg);
  transform: rotate(45deg);
}
</style>


