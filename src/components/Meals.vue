<template>
  <div v-if="meals.length" class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-3 gap-6 px-5 sm:px-8">
    <MealItem v-for="meal of meals" :key="meal.idMeal" :meal="meal" />
  </div>
  <div v-else class="mx-5 sm:mx-8 rounded-2xl border border-dashed border-stone-300 py-14 text-center text-stone-500">
    No meals to show yet.
  </div>
</template>

<script setup>
import MealItem from './MealItem.vue';

const { meals } = defineProps({
  meals: {
    required: true,
    type: Array,
  }
})

</script>
