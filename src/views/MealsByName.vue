<template>
  <div class="px-5 sm:px-8 pt-9 pb-6">
    <p class="text-sm font-bold uppercase tracking-[0.16em] text-[#315c49]">Recipe finder</p>
    <h1 class="mt-2 mb-6 text-3xl sm:text-4xl font-black text-[#24312b]">Search meals</h1>
    <div class="relative max-w-2xl">
    <input
      type="text"
      v-model="keyword"
        class="h-14 w-full rounded-xl border border-stone-300 bg-white pl-12 pr-4 text-base shadow-sm outline-none transition focus:border-[#315c49] focus:ring-4 focus:ring-[#315c49]/10"
        placeholder="Try chicken, pasta or soup..."
      @change="searchMeals"
    />
      <span class="pointer-events-none absolute left-4 top-1/2 -translate-y-1/2 text-stone-400" aria-hidden="true">
        <svg width="18" height="18" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
          <circle cx="11" cy="11" r="7"></circle>
          <path d="m20 20-3.5-3.5"></path>
        </svg>
      </span>
    </div>
  </div>

  <p v-if="isLoading" class="px-8 pb-5 text-stone-500">Searching the recipe collection...</p>
  <p v-if="errorMessage" class="mx-8 mb-5 rounded-xl bg-red-50 px-4 py-3 text-red-700">{{ errorMessage }}</p>
  <Meals :meals="meals" />
</template>

<script setup>
import { onMounted, ref } from "vue";
import { useRoute } from "vue-router";
import Meals from '../components/Meals.vue'
import axiosClient from "../axiosClient";

const route = useRoute();
const keyword = ref("");
const meals = ref([]);
const isLoading = ref(false);
const errorMessage = ref("");

async function searchMeals() {
  meals.value = [];
  errorMessage.value = "";

  if (!keyword.value.trim()) {
    return;
  }

  isLoading.value = true;
  try {
    const { data } = await axiosClient.get(
      `search.php?s=${encodeURIComponent(keyword.value)}`
    );
    meals.value = data.meals || [];
  } catch (error) {
    errorMessage.value = "Could not search meals.";
  } finally {
    isLoading.value = false;
  }
}

onMounted(() => {
  keyword.value = route.params.name
  if (keyword.value) {
    searchMeals()
  }
})
</script>
