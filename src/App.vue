<script setup>
import {ref, watch} from 'vue'

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
</script>




<template>
<h1>My Todo Application</h1>
<li v-for="(todo, index) in todos" :class="{completed: todo.complete}">
  <input type="checkbox" v-model="todo.complete">
  <button @click="deleteI(index)">🗑</button>
  {{todo.text}}
</li>
<input v-model="touch" @keydown.enter="uno">
<button @click="uno">Add Todo</button>
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
      background-color: rgb(26, 255, 0);
      text-decoration: line-through;


}
</style>


