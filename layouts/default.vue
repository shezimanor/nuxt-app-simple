<script lang="ts" setup></script>

<template>
  <nav class="flex gap-x-2">
    <ULink
      to="/"
      active-class="text-blue-800"
      inactive-class="text-gray-500 dark:text-gray-400 hover:text-gray-700 dark:hover:text-gray-200"
    >
      Home
    </ULink>
    <ULink
      to="/virtual-list"
      active-class="text-blue-800"
      inactive-class="text-gray-500 dark:text-gray-400 hover:text-gray-700 dark:hover:text-gray-200"
    >
      VirtualList
    </ULink>
  </nav>
  <UContainer>
    <slot />
  </UContainer>
</template>

<style scoped></style>
