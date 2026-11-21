<template>
  <div class="px-5 sm:px-8 pt-9 pb-6">
    <p class="text-sm font-bold uppercase tracking-[0.16em] text-[#315c49]">Browse the collection</p>
    <h1 class="mt-2 mb-6 text-3xl sm:text-4xl font-black text-[#24312b]">Meals by letter</h1>
  <div class="flex flex-wrap gap-2">
    <router-link
      :to="{ name: 'byLetter', params: { letter } }"
      v-for="letter of letters"
      :key="letter"
      class="grid h-10 w-10 place-items-center rounded-full border border-stone-200 bg-white text-sm font-bold text-stone-600 transition hover:border-[#315c49] hover:text-[#315c49]"
      :class="{ 'border-[#315c49] bg-[#315c49] text-white hover:text-white': route.params.letter === letter }"
    >
      {{ letter }}
    </router-link>
  </div>
  </div>

  <p v-if="isLoading" class="px-8 pb-5 text-stone-500">Loading meals...</p>
  <p v-if="errorMessage" class="mx-8 mb-5 rounded-xl bg-red-50 px-4 py-3 text-red-700">{{ errorMessage }}</p>
  <Meals :meals="meals" />
</template>

<script setup>
import { onMounted, ref, watch } from "vue";
import { useRoute } from "vue-router";
import axiosClient from "../axiosClient";
import Meals from "../components/Meals.vue";

const route = useRoute();
const letters = "ABCDEFGHIJKLMNOPQRSTUVWXYZ".split("");
const meals = ref([]);
const isLoading = ref(false);
const errorMessage = ref("");

async function loadMeals(letter) {
  meals.value = [];
  errorMessage.value = "";

  if (!letter) {
    return;
  }

  isLoading.value = true;
  try {
    const { data } = await axiosClient.get(`search.php?f=${encodeURIComponent(letter)}`);
    meals.value = data.meals || [];
  } catch (error) {
    errorMessage.value = "Could not load meals.";
  } finally {
    isLoading.value = false;
  }
}

watch(() => route.params.letter, loadMeals);

onMounted(() => {
  loadMeals(route.params.letter);
});
</script>
