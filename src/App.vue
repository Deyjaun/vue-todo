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
</script>




<template>
<h1>My Todo Application</h1>
<li v-for="(todo, index) in todos.filter(todoFilter)" :class="{completed: todo.complete}">
  <label class="container"><input type="checkbox" v-model="todo.complete"><span class="checkmark"></span></label>
  <button @click="deleteI(index)">🗑</button>
  {{todo.text}}
</li>
<input v-model="touch" @keydown.enter="uno">
<button @click="uno">Add Todo</button>
<hr>

<input name="filter" type="radio"  value="all" v-model="filter">
<label>All</label>


<input name="filter" type="radio"  value="active" v-model="filter">
<label>Active</label>


<input name="filter" type="radio"  value="complete" v-model="filter">
<label>Complete</label>


</template>

<style>
body {
  font-weight: bold;
    font-size: large;
color: #000000;
background-color: #0037ff;
background-image: url("data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' width='100%25' height='100%25' viewBox='0 0 1600 800'%3E%3Cg stroke='%23FFFFFF' stroke-width='100' stroke-opacity='0' %3E%3Ccircle fill='%230D00FF' cx='0' cy='0' r='1800'/%3E%3Ccircle fill='%230034ff' cx='0' cy='0' r='1700'/%3E%3Ccircle fill='%23004cff' cx='0' cy='0' r='1600'/%3E%3Ccircle fill='%23005eff' cx='0' cy='0' r='1500'/%3E%3Ccircle fill='%23006dff' cx='0' cy='0' r='1400'/%3E%3Ccircle fill='%23007aff' cx='0' cy='0' r='1300'/%3E%3Ccircle fill='%230087ff' cx='0' cy='0' r='1200'/%3E%3Ccircle fill='%230092ff' cx='0' cy='0' r='1100'/%3E%3Ccircle fill='%23009dff' cx='0' cy='0' r='1000'/%3E%3Ccircle fill='%2300a8ff' cx='0' cy='0' r='900'/%3E%3Ccircle fill='%2300b1ff' cx='0' cy='0' r='800'/%3E%3Ccircle fill='%2300bbff' cx='0' cy='0' r='700'/%3E%3Ccircle fill='%2300c4ff' cx='0' cy='0' r='600'/%3E%3Ccircle fill='%2300cdff' cx='0' cy='0' r='500'/%3E%3Ccircle fill='%2300d6ff' cx='0' cy='0' r='400'/%3E%3Ccircle fill='%2300deff' cx='0' cy='0' r='300'/%3E%3Ccircle fill='%2300e6ff' cx='0' cy='0' r='200'/%3E%3Ccircle fill='%2300EEFF' cx='0' cy='0' r='100'/%3E%3C/g%3E%3C/svg%3E");
background-attachment: fixed;
background-size: cover;
}
button {
    color: rgb(255, 255, 255);
    background-color: rgb(1, 197, 251);
    font-size: 85%;
    font-weight: bold;
    border-radius: 15%;
    border-color: rgb(85, 0, 255);
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


