<template>
  <Navbar />
  <main class="min-h-[calc(100vh-72px)]">
    <div class="max-w-[1180px] mx-auto pb-12">
      <router-view />
    </div>
  </main>
</template>

<script setup>
import Navbar from "../components/Navbar.vue";
</script>
