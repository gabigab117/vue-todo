<template>

  <h1>Todo</h1>

  <form action="" @submit.prevent="createTodo(newTodo)">
    <input type="text" v-model="newTodo"> 
    <button :disabled="newTodo.length === 0">Ajouter</button> <!--Desactiver le bouton si vide-->
    {{ newTodo }}
  </form>




<div v-if="todos.length >= 1">
  <table>
  <caption>
    Tableau des tâches
  </caption>
  <thead>
    <tr>
      <th scope="col">Titre</th>
      <th scope="col">Fait ?</th>
      <th scope="col">Date</th>
    </tr>
  </thead>
  <tbody>
    <tr
    v-for="todo in sortedTodos()"
    :key="todo.date"
    >
      <th :class="{maclasse: todo.completed}" scope="row">{{ todo.title }}</th>
      <td>
      <label>
        <input type="checkbox" v-model="todo.completed" />
        {{ todo.completed }}
      </label>
      <!---->
      </td>
      <td>{{ todo.date }}</td>
    </tr>
  </tbody>
  </table>
    <label>
      <input type="checkbox" v-model="hideCompleted" />
      Masquer les tâches terminées
    </label>
</div>
<div v-else>
Pas de tâches
</div>

</template>


<script setup>
import { ref } from 'vue';

const todos = ref([
  {
    title: "tâche1",
    completed: true,
    date: 1020302103
  }
])

const newTodo = ref("")
const hideCompleted = ref(false)

const createTodo = title => {
  todos.value.push({title: title, completed: false, date: Date.now()})
  newTodo.value = "" // vider l'input
}

const sortedTodos = () => {
  const sortedTodos =  todos.value.toSorted((a, b) => a.completed > b.completed ? 1 : -1) // ne modifie pas le tableau mais l'organise. Avec une fonction de comparaison
  if (hideCompleted.value === true) {
    return sortedTodos.filter(t => t.completed === false) // Important le filter super !
  }
  return sortedTodos // C'est la hideCompleted dans la checkbox qui va faire le tri
}
</script>


<style>
.maclasse {
  text-decoration: line-through;
}

table {
  border-collapse: collapse;
  border: 2px solid rgb(140 140 140);
  font-family: sans-serif;
  font-size: 0.8rem;
  letter-spacing: 1px;
}

caption {
  caption-side: bottom;
  padding: 10px;
  font-weight: bold;
}

thead,
tfoot {
  background-color: rgb(228 240 245);
}

th,
td {
  border: 1px solid rgb(160 160 160);
  padding: 8px 10px;
}

td:last-of-type {
  text-align: center;
}

tbody > tr:nth-of-type(even) {
  background-color: rgb(237 238 242);
}

tfoot th {
  text-align: right;
}

tfoot td {
  font-weight: bold;
}

</style>