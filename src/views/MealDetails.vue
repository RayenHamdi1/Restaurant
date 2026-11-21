<template>
  <div class="mx-5 sm:mx-8 my-8 max-w-[1000px]">
    <p v-if="isLoading" class="text-stone-500">Loading meal...</p>
    <p v-if="errorMessage" class="rounded-xl bg-red-50 px-4 py-3 text-red-700">{{ errorMessage }}</p>
    <template v-if="meal.idMeal">
      <div class="overflow-hidden rounded-[28px] border border-stone-200 bg-white">
        <img :src="meal.strMealThumb" :alt="meal.strMeal" class="h-72 sm:h-[420px] w-full object-cover">
        <div class="p-6 sm:p-9">
          <p class="mb-2 text-sm font-bold uppercase tracking-[0.16em] text-[#315c49]">{{ meal.strCategory }}</p>
          <h1 class="text-3xl sm:text-5xl font-black leading-tight text-[#24312b]">{{ meal.strMeal }}</h1>
          <div class="mt-5 flex flex-wrap gap-2">
            <span class="rounded-full bg-[#edf1ed] px-3 py-1.5 text-sm font-semibold text-[#315c49]">{{ meal.strArea }}</span>
            <span v-if="meal.strTags" class="rounded-full bg-[#f7f1dc] px-3 py-1.5 text-sm font-semibold text-[#725d16]">{{ meal.strTags }}</span>
          </div>

          <div class="mt-8 grid gap-8 lg:grid-cols-[1fr_0.72fr]">
            <section>
              <h2 class="mb-3 text-xl font-black text-[#24312b]">Instructions</h2>
              <p class="whitespace-pre-line leading-7 text-stone-600">{{ meal.strInstructions }}</p>
            </section>
            <aside class="rounded-2xl bg-[#f7f5ef] p-5">
              <h2 class="mb-4 text-xl font-black text-[#24312b]">Ingredients</h2>
              <ul class="space-y-2 text-sm text-stone-600">
                <li
                  v-for="item in ingredients"
                  :key="item.name"
                  class="border-b border-stone-200 pb-2"
                >
                    <strong class="text-[#24312b]">{{ item.measure }}</strong>
                    {{ item.name }}
                  </li>
              </ul>
            </aside>
          </div>

          <div v-if="meal.strYoutube || meal.strSource" class="mt-8 flex flex-wrap gap-3 border-t border-stone-200 pt-6">
            <YouTubeButton v-if="meal.strYoutube" :href="meal.strYoutube" />
            <a
              v-if="meal.strSource"
              :href="meal.strSource"
              target="_blank"
              rel="noopener noreferrer"
              class="rounded-lg border border-stone-300 px-3 py-2 text-xs font-bold text-stone-700 transition hover:border-[#315c49] hover:text-[#315c49]"
            >
              View original source
            </a>
          </div>
        </div>
      </div>
    </template>
  </div>
</template>

<script setup>
import { onMounted, ref, watch } from 'vue'
import { useRoute } from 'vue-router';
import axiosClient from '../axiosClient';
import YouTubeButton from '../components/YouTubeButton.vue';

const route = useRoute();
const meal = ref({})
const ingredients = ref([])
const isLoading = ref(false)
const errorMessage = ref("")

async function loadMeal(id) {
  meal.value = {}
  errorMessage.value = ""
  isLoading.value = true

  try {
    const { data } = await axiosClient.get(`lookup.php?i=${id}`)
    meal.value = data.meals[0] || {}
    ingredients.value = []

    for (let i = 1; i <= 20; i++) {
      const name = meal.value[`strIngredient${i}`]
      const measure = meal.value[`strMeasure${i}`]

      if (name) {
        ingredients.value.push({
          name,
          measure
        })
      }
    }
  } catch (error) {
    errorMessage.value = "Could not load meal details."
  } finally {
    isLoading.value = false
  }
}

watch(() => route.params.id, loadMeal)
onMounted(() => loadMeal(route.params.id))

</script>