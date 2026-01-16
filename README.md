# Nuxt Learning Project

Created this small Nuxt project to get familiar with the Nuxt setup and some of the core concepts.

The focus of this project was learning:

- Nuxt file-based routing (pages vs components)
- Vue 3 Composition API using `<script setup>`
- Passing data via props and handling events with emits
- Basic data fetching and local state management
- Running and building a Nuxt app locally

---

## Pages

The application runs locally on the default Nuxt port:

- Articles page: http://localhost:3000/
- Todo page: http://localhost:3000/todo

---

## Tech Stack Used

- Nuxt (Vue 3)
- TypeScript
- Bootstrap
- Yarn

---

## What’s in the Project

### Articles Page

- Loads article data from a static JSON file in the `public/` directory
- Handles loading and error states
- Uses a reusable `ArticleCard` component to display each article

### Todo Page

- Simple todo example to understand component communication
- Uses `v-model` for controlled inputs
- Page owns the state while child components emit events for updates

---

## Setup

Install dependencies:

```bash
yarn install
```
