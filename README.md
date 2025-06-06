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
- `Layout.vue`: Composant de mise en page utilisant CSS Grid et les slots nommés.
- `Checkbox.vue`: Composant réutilisable de checkbox avec support des événements personnalisés.
- `Button.vue`: Composant de bouton réutilisable utilisant les slots pour le contenu.

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

## Composants Réutilisables

L'application utilise plusieurs composants réutilisables pour structurer le code et améliorer la maintenabilité :

### Layout.vue
Composant de mise en page utilisant CSS Grid pour créer une structure de page avec header, sidebar, contenu principal et footer :

- **Structure Grid** : Utilise `display: grid` avec `grid-template-columns: 200px 1fr` pour créer une sidebar de 200px et un contenu principal flexible
- **Slots nommés** : Utilise 4 slots nommés pour organiser le contenu :
  - `header` : En-tête (prend toute la largeur avec `grid-column: 1 / -1`)
  - `aside` : Barre latérale (200px de largeur)
  - `main` : Contenu principal (largeur flexible)
  - `footer` : Pied de page (prend toute la largeur)
- **Conditional rendering** : Utilise `v-if="$slots.header"` pour n'afficher l'élément header que si du contenu lui est fourni

### Button.vue
Composant de bouton simple et réutilisable :

- **Slot par défaut** : Utilise `<slot></slot>` pour permettre l'insertion de contenu personnalisé, y compris du HTML (ex: `<strong>Demo</strong> de bouton`)
- **Style** : Applique une classe CSS `secondary` par défaut

### Checkbox.vue
Composant de checkbox avancé avec gestion d'état bidirectionnelle :

- **defineModel()** : Utilise la nouvelle API Vue 3 pour établir une connexion bidirectionnelle avec `v-model`
- **Props** : Accepte une prop `label` pour le texte d'affichage
- **Événements personnalisés** : Émet `check` et `uncheck` avec l'élément checkbox comme paramètre
- **Flexibilité** : Peut être utilisé avec ou sans v-model, avec des labels statiques ou dynamiques

## Utilisation des Slots

L'application démontre l'utilisation des slots Vue.js pour créer des composants flexibles :

- **Slots nommés** dans `Layout.vue` pour organiser différentes sections de la page
- **Slot par défaut** dans `Button.vue` pour permettre du contenu HTML personnalisé
- **Template syntax** : Utilisation de `<template #slotName>` dans `App.vue` pour passer du contenu aux slots nommés

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