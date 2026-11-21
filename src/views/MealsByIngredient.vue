<template>
  <div class="px-5 sm:px-8 pt-9 pb-6">
    <p class="text-sm font-bold uppercase tracking-[0.16em] text-[#315c49]">Ingredient collection</p>
    <h1 class="mt-2 text-3xl sm:text-4xl font-black text-[#24312b]">
      Meals with {{ route.params.ingredient }}
    </h1>
  </div>

  <p v-if="isLoading" class="px-8 pb-5 text-stone-500">Loading meals...</p>
  <p v-if="errorMessage" class="mx-8 mb-5 rounded-xl bg-red-50 px-4 py-3 text-red-700">{{ errorMessage }}</p>
  <Meals :meals="meals" />
</template>

<script setup>
import { onMounted, ref, watch } from "vue";
import { useRoute } from "vue-router";
import axiosClient from "../axiosClient";
import Meals from '../components/Meals.vue'

const route = useRoute();
const meals = ref([]);
const isLoading = ref(false);
const errorMessage = ref("");

async function loadMeals(ingredient) {
  meals.value = [];
  errorMessage.value = "";
  isLoading.value = true;

  try {
    const { data } = await axiosClient.get(`filter.php?i=${encodeURIComponent(ingredient)}`);
    meals.value = data.meals || [];
  } catch (error) {
    errorMessage.value = "Could not load meals.";
  } finally {
    isLoading.value = false;
  }
}

watch(() => route.params.ingredient, loadMeals);

onMounted(() => {
  loadMeals(route.params.ingredient);
})

</script>
