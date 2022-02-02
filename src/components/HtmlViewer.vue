<script setup lang="ts">
defineProps<{
  htmlContent: string;
}>();
</script>

<template>
  <div id="html-preview" v-html="htmlContent"></div>
</template>

<style scoped>
#html-preview:deep(h1) {
  @apply font-bold text-4xl;
}
</style>
