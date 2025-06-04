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