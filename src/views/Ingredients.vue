<template>
  <div class="px-5 sm:px-8 pt-9 pb-7">
    <p class="text-sm font-bold uppercase tracking-[0.16em] text-[#315c49]">Browse by pantry</p>
    <h1 class="mt-2 mb-6 text-3xl sm:text-4xl font-black text-[#24312b]">Ingredients</h1>
    <input
      type="text"
      v-model="keyword"
      class="h-14 max-w-2xl rounded-xl border border-stone-300 bg-white px-4 text-base shadow-sm outline-none transition focus:border-[#315c49] focus:ring-4 focus:ring-[#315c49]/10"
      placeholder="Filter ingredients..."
    />
  </div>
  <div class="px-5 sm:px-8">
    <p v-if="isLoading" class="pb-5 text-stone-500">Loading ingredients...</p>
    <p v-if="errorMessage" class="mb-5 rounded-xl bg-red-50 px-4 py-3 text-red-700">{{ errorMessage }}</p>
    <div class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-3 gap-3">
      <button
        type="button"
        @click.prevent="openIngredient(ingredient)"
        v-for="ingredient of computedIngredients"
        :key="ingredient.idIngredient"
        class="flex items-center justify-between rounded-xl border border-stone-200 bg-white px-5 py-4 text-left transition hover:border-[#315c49] hover:bg-[#edf1ed]"
      >
        <h3 class="font-bold text-[#24312b]">{{ ingredient.strIngredient }}</h3>
        <span class="text-[#315c49]" aria-hidden="true">→</span>
      </button>
    </div>
  </div>
</template>

<script setup>
import { computed } from "vue";
import { onMounted, ref } from "vue";
import { useRouter } from "vue-router";
import axiosClient from "../axiosClient";

const router = useRouter();
const keyword = ref("");
const ingredients = ref([]);
const isLoading = ref(true);
const errorMessage = ref("");
const computedIngredients = computed(() => {
  if (!keyword.value) return ingredients.value;
  return ingredients.value.filter((i) =>
    i.strIngredient.toLowerCase().includes(keyword.value.toLowerCase())
  );
});

function openIngredient(ingredient) {
  router.push({
    name: "byIngredient",
    params: { ingredient: ingredient.strIngredient },
  });
}

onMounted(() => {
  axiosClient
    .get("list.php?i=list")
    .then(({ data }) => {
      ingredients.value = data.meals || [];
    })
    .catch(() => {
      errorMessage.value = "Could not load ingredients.";
    })
    .finally(() => {
      isLoading.value = false;
    });
});
</script>
