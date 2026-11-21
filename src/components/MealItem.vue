<template>
  <article class="group overflow-hidden rounded-2xl border border-stone-200 bg-white transition duration-300 hover:-translate-y-1 hover:shadow-[0_18px_40px_-24px_rgba(36,49,43,0.35)]">
    <router-link :to="{ name: 'mealDetails', params: { id: meal.idMeal } }" class="block overflow-hidden">
      <img
        :src="meal.strMealThumb"
        :alt="meal.strMeal"
        class="h-52 w-full object-cover transition duration-500 group-hover:scale-[1.03]"
      />
    </router-link>
    <div class="p-5">
      <router-link :to="{ name: 'mealDetails', params: { id: meal.idMeal } }">
        <h3 class="mb-2 line-clamp-2 text-lg font-bold leading-snug text-[#24312b] hover:text-[#315c49]">{{ meal.strMeal }}</h3>
      </router-link>
      <p class="mb-5 min-h-[40px] text-sm leading-5 text-stone-500">
        {{ shortInstructions }}
      </p>
      <div class="flex items-center justify-between gap-3 border-t border-stone-100 pt-4">
        <router-link
          :to="{ name: 'mealDetails', params: { id: meal.idMeal } }"
          class="text-sm font-bold text-[#315c49]"
        >
          View recipe
        </router-link>
        <YouTubeButton v-if="meal.strYoutube" :href="meal.strYoutube" />
      </div>
    </div>
  </article>
</template>

<script setup>
import { computed } from "vue";
import YouTubeButton from './YouTubeButton.vue';

const { meal } = defineProps({
  meal: {
    required: true,
    type: Object
  }
})
const shortInstructions = computed(() => {
  if (!meal.strInstructions) return "";
  return meal.strInstructions.split(" ").slice(0, 20).join(" ");
})

</script>
