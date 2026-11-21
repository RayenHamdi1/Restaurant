<template>
  <a
    :href="href"
    target="_blank"
    rel="noopener noreferrer"
    class="rounded-lg border border-[#315c49] px-3 py-2 text-xs font-bold text-[#315c49] transition-colors hover:bg-[#315c49] hover:text-white"
  >
    <slot>YouTube</slot>
  </a>
</template>

<script setup>
const props = defineProps({
  href: String
})
</script>
