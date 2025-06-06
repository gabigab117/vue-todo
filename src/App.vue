<template>

  <Layout>

      <template #aside>
      Sidebar
    </template>
      <template #main>
      Contenu principal
    </template>
      <template #footer>
      Pied de page
    </template>
  </Layout>

  <Button><strong>Demo</strong> de bouton</Button>

  <h1>Todo</h1>

  <form action="" @submit.prevent="createTodo(newTodo)">
    <input type="text" v-model="newTodo"> 
    <button :disabled="!newTodo.length">Ajouter</button> <!--Desactiver le bouton si vide-->
    {{ newTodo }}
  </form>




<div v-if="todos.length >= 1">
    <ul>
      <li 
      v-for ="todo in sortedTodos"
      :key="todo.date"
      :class="{maclasse: todo.completed}"
      >

      <Checkbox :label="todo.title" 
      class="class1" 
      @check="(p) => console.log('coché', p)"
      @uncheck="console.log('pas coché')"
      v-model="todo.completed"
      /> <!--J'envoie des éléments dynamiques--> <!-- passage implicite avec class qui s'applique au premier élément du template -->
      <!--Avec label je fais descendre des infos-->
      </li>
    </ul>
    <label>
      <input type="checkbox" v-model="hideCompleted" />
      Masquer les tâches terminées
    </label>
    <p v-if="remainingTodos">Nombre de tâche{{ remainingTodos > 1 ? "s" : "" }} à faire {{ remainingTodos }}</p>

    <Checkbox label="Bonjour" />

</div>
<div v-else>
Pas de tâches
</div>

</template>


<script setup>

import { ref, computed } from 'vue';
import Checkbox from './Checkbox.vue';
import Button from './Button.vue';
import Layout from './Layout.vue';

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

const sortedTodos = computed(() => { // computed permet de ne pas appeler la fonction à chaque fois que le composant est rendu et plus besoin des parenthèses dans le html
  // ça dérive de todos, donc computed va se mettre à jour si todos change
  const sortedTodos =  todos.value.toSorted((a, b) => a.completed > b.completed ? 1 : -1) // ne modifie pas le tableau mais l'organise. Avec une fonction de comparaison
  if (hideCompleted.value === true) { // toSorted car avec un computed pas de mutation !
    return sortedTodos.filter(t => t.completed === false) // Important le filter super !
  }
  return sortedTodos // C'est la hideCompleted dans la checkbox qui va faire le tri
})

const remainingTodos = computed(() => {
  return todos.value.filter(t => !t.completed).length
})

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