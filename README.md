# Restaurant Vue

**Live demo:** https://restaurentmeals.vercel.app

A small recipe browser built with Vue 3, Vue Router, Vuex and Tailwind CSS. It uses
[TheMealDB](https://www.themealdb.com/) as its data source.

## Features

- Search meals by name
- Browse meals by first letter
- Browse meals by main ingredient
- Meal details page with ingredients, instructions and a YouTube link

## Tech stack

- Vue 3 (`<script setup>`)
- Vue Router 4
- Vuex 4
- Axios
- Tailwind CSS
- Vite

## Getting started

```bash
npm install
cp .env.example .env   # on Windows: copy .env.example .env
npm run dev
```

The app runs on the Vite dev server (default http://localhost:5173).

## Environment variables

| Variable             | Description             | Default                                      |
| -------------------- | ----------------------- | -------------------------------------------- |
| `VITE_API_BASE_URL`  | Base URL of TheMealDB   | `https://www.themealdb.com/api/json/v1/1/`   |

## Scripts

| Script          | Description               |
| --------------- | ------------------------- |
| `npm run dev`   | Start the dev server      |
| `npm run build` | Build for production      |
| `npm run preview` | Preview the build       |

## Project structure

```
src/
  components/   Layout, navbar and meal related components
  views/        Home, search, ingredients and meal details pages
  router/       Route definitions
  store/        Vuex state, mutations and actions
  filters/      Shared template filters
  axiosClient.js
```

## API

All data comes from TheMealDB, a free and open recipe API. No key is required.

