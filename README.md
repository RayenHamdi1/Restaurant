# Savor

Savor is a small meal and recipe browser made with Vue 3. It is a front-end project:
it does not use its own server or database. Recipe information comes from
[TheMealDB](https://www.themealdb.com/) through a public API.

## What you can do

- Browse random meals on the home page
- Search for meals by name
- Browse meals alphabetically
- Choose an ingredient and see related meals
- Open a recipe to view ingredients and instructions
- Watch a linked YouTube video or open the original recipe source

## Technologies used

- Vue 3
- Vue Router
- Axios
- Tailwind CSS
- Vite

## Running locally

Make sure Node.js and npm are installed. Then open the project folder in a terminal:

```bash
npm install
npm run dev
```

Visit the address printed in the terminal. It is usually `http://localhost:5173`.

No API key is needed. The application uses the TheMealDB address defined in
`src/axiosClient.js`.

## Production build

```bash
npm run build
npm run preview
```

The build is created in the `dist` folder.

## Project files

```text
src/
  components/    Shared layout and meal cards
  views/         Pages for home, search and recipes
  router/        Application routes
  axiosClient.js Axios configuration
  style.css      Global styles
```

The main routes are `/`, `/by-name`, `/by-letter`, `/ingredients`,
`/by-ingredient/:ingredient`, and `/meal/:id`.
