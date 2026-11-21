<template>
  <header class="border-b border-stone-200 bg-[#fdfcf8]/95 sticky top-0 z-30 backdrop-blur">
    <nav class="max-w-[1180px] mx-auto px-5 sm:px-8 h-18 min-h-[72px] flex items-center justify-between gap-5">
    <router-link
      :to="{ name: 'home' }"
        class="flex items-center gap-2.5 shrink-0"
    >
        <span class="grid h-9 w-9 place-items-center rounded-full bg-[#315c49] text-sm font-bold text-white">S</span>
        <span class="text-xl font-black tracking-tight text-[#24312b]">Savor</span>
    </router-link>
      <div class="flex items-center gap-1 overflow-x-auto">
      <router-link
        :to="{ name: 'byName' }"
          class="nav-link"
      >
          Search
      </router-link>
      <router-link
        :to="{ name: 'byLetter' }"
          class="nav-link"
      >
          A-Z
      </router-link>
      <router-link
        :to="{ name: 'ingredients' }"
          class="nav-link"
      >
          Ingredients
      </router-link>
    </div>
    </nav>
  </header>
</template>

<style scoped>
.nav-link {
  @apply whitespace-nowrap rounded-full px-3.5 py-2 text-sm font-semibold text-stone-600 transition;
}

.nav-link:hover {
  @apply bg-[#edf1ed] text-[#315c49];
}

.router-link-active.nav-link {
  @apply bg-[#315c49] text-white;
}
</style>
