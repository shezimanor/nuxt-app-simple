<script lang="ts" setup>
const list = Array.from({ length: 15 }, (_, i) => `list item: ${i}`);
</script>

<template>
  <main>
    <h1>Virtual List Page</h1>
    <VirtualList :list="list" :item-height="100" :window-height="500" />
  </main>
</template>

<style scoped></style>
