# Restaurant Vue

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

## Deployment

The project is ready to deploy on [Vercel](https://vercel.com):

1. Go to [vercel.com/new](https://vercel.com/new) and import the `Restaurent` repository.
2. Vercel auto-detects Vite. Keep the defaults (build `npm run build`, output `dist`).
3. Optionally add `VITE_API_BASE_URL` as an environment variable. The app falls back to
   `https://www.themealdb.com/api/json/v1/1/` when it is not set.
4. Deploy.

`vercel.json` adds a SPA rewrite so deep links such as `/meal/52772` work on refresh.
