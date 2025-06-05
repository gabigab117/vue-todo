# Todo Grafik

## Description

This is a simple Todo application built with Vue.js. It allows users to manage their tasks efficiently by adding, viewing, and marking tasks as completed. The application also provides a feature to hide completed tasks.

## Features

- Add new tasks with a title.
- View tasks in a table format with columns for title, completion status, and date.
- Mark tasks as completed using a checkbox.
- Hide completed tasks with a toggle option.
- Tasks are sorted by their completion status.

## Project Structure

- `App.vue`: Contains the main application logic and UI.

## Computed Properties

L'application utilise des propriétés calculées (computed) pour optimiser les performances et gérer l'état dérivé :

- **`sortedTodos`** : Trie les tâches par statut de completion (tâches non terminées en premier) et filtre les tâches terminées selon l'option de masquage. Cette computed property se met automatiquement à jour lorsque la liste des tâches ou l'option de masquage change.

- **`remainingTodos`** : Calcule le nombre de tâches restantes à accomplir en filtrant les tâches non terminées. Utilisée pour afficher le compteur de tâches restantes dans l'interface.

Ces computed properties permettent d'éviter les recalculs inutiles et s'actualisent automatiquement uniquement lorsque leurs dépendances changent.

## Props et Emits

L'application utilise le système de communication parent-enfant de Vue.js avec les props et emits :

### Props
Les **props** permettent de faire descendre des données du composant parent vers le composant enfant :

- **`Checkbox.vue`** : Reçoit une prop `label` de type `String` depuis `App.vue`
  - Utilisée pour afficher le texte associé à la checkbox
  - Déclarée avec `defineProps({ label: String })`
  - Utilisée de deux façons différentes dans l'application :
    - Avec une chaîne statique : `<Checkbox label="Bonjour" />`
    - Avec la propriété dynamique d'un objet : `:label="todo.title"` (le titre de chaque tâche)

### Emits
Les **emits** permettent à un composant enfant de communiquer avec son parent en émettant des événements :

- **`Checkbox.vue`** : Émet deux événements vers `App.vue`
  - `check` : Émis quand la checkbox est cochée, avec `event.currentTarget` comme paramètre
  - `uncheck` : Émis quand la checkbox est décochée, avec `event.currentTarget` comme paramètre
  - Déclarés avec `defineEmits(["check", "uncheck"])`

### Utilisation dans App.vue
Le composant parent `App.vue` utilise le composant `Checkbox` en :
- Passant des données via les props : `:label="todo.title"`
- Écoutant les événements émis : `@check="(p) => console.log('coché', p)"` et `@uncheck="console.log('pas coché')"`

Cette architecture permet une communication claire et unidirectionnelle entre les composants, respectant les bonnes pratiques de Vue.js.

## How to Run

1. Clone the repository.
2. Install dependencies using `npm install`.
3. Start the development server with `npm run dev`.
4. Open the application in your browser at the provided local URL.

## Technologies Used

- Vue.js 3
- Vite
- JavaScript
- HTML/CSS