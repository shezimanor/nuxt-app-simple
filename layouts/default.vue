<script lang="ts" setup></script>

<template>
  <nav>
    <ULink
      to="/"
      active-class="text-blue-800"
      inactive-class="text-gray-500 dark:text-gray-400 hover:text-gray-700 dark:hover:text-gray-200"
    >
      Home
    </ULink>
  </nav>
  <UContainer>
    <slot />
  </UContainer>
</template>

<style scoped></style>
