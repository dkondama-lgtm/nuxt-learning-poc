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
## Preview
<img width="1134" height="684" alt="3" src="https://github.com/user-attachments/assets/75ad9fec-ee1a-4e92-997a-a7596c7c171e" />
<img width="753" height="364" alt="4" src="https://github.com/user-attachments/assets/a1439cac-a8ef-465d-9c14-9a9190667b0f" />
<img width="753" height="337" alt="1" src="https://github.com/user-attachments/assets/d74edbe0-5c11-4ebc-9e82-82573fc5c527" />
<img width="754" height="385" alt="2" src="https://github.com/user-attachments/assets/224ff67c-bdb1-46d1-90c1-14ad57f28728" />

