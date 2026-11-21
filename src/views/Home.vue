<template>
  <section class="mx-5 sm:mx-8 mt-8 mb-8 overflow-hidden rounded-[28px] bg-[#315c49] px-7 py-10 text-white sm:px-10">
    <p class="mb-2 text-sm font-bold uppercase tracking-[0.18em] text-[#bcd4c5]">Discover something delicious</p>
    <h1 class="max-w-xl text-3xl sm:text-5xl font-black leading-tight">What will you cook today?</h1>
    <router-link
      :to="{ name: 'byName' }"
      class="mt-7 inline-flex rounded-full bg-[#f2c94c] px-5 py-3 text-sm font-bold text-[#24312b] transition hover:bg-[#ffe27a]"
    >
      Search recipes
    </router-link>
  </section>
  <div class="px-5 sm:px-8 mb-5 flex items-end justify-between">
    <div>
      <p class="text-sm font-bold text-[#315c49]">Fresh inspiration</p>
      <h2 class="mt-1 text-2xl font-black text-[#24312b]">Random picks</h2>
    </div>
  </div>
  <p v-if="isLoading" class="px-8 py-6 text-stone-500">Loading meals...</p>
  <p v-if="errorMessage" class="mx-8 rounded-xl bg-red-50 px-4 py-3 text-red-700">{{ errorMessage }}</p>
  <Meals :meals="meals" />
</template>

<script setup>
import { onMounted, ref } from "vue";
import Meals from "../components/Meals.vue";
import axiosClient from "../axiosClient.js";

const meals = ref([]);
const isLoading = ref(true);
const errorMessage = ref("");

onMounted(async () => {
  try {
    for (let i = 0; i < 6; i++) {
      const response = await axiosClient.get("random.php");
      meals.value.push(response.data.meals[0]);
    }
  } catch (error) {
    errorMessage.value = "Could not load random meals.";
  }

  isLoading.value = false;
});
</script>
