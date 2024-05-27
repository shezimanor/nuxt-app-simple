<script lang="ts" setup>
const list = Array.from({ length: 3000 }, (_, i) => ({
  data: `list item: ${i}`,
  id: i
}));
</script>

<template>
  <main>
    <h1>Virtual List Page</h1>
    <VirtualList :list="list" :item-height="50" />
  </main>
</template>

<style scoped></style>
