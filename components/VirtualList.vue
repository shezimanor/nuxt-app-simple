<script lang="ts" setup>
const props = defineProps({
  list: {
    type: Array,
    required: true,
    default: () => []
  },
  itemHeight: {
    type: Number,
    default: 100
  },
  windowHeight: {
    type: Number,
    default: 500
  }
});
const itemCount = computed(() => props.list.length);
const onScroll = (e: Event) => {
  const target = e.target as HTMLElement;
  console.log(target.scrollTop);
};
</script>

<template>
  <div
    class="v-window"
    :style="{
      height: `${windowHeight}px`
    }"
    @scroll="onScroll"
  >
    <ul
      class="v-list"
      :style="{
        height: `${itemCount * itemHeight}px`
      }"
    >
      <li
        v-for="(item, index) in list"
        :key="index"
        class="v-item"
        :style="{
          top: `${index * itemHeight}px`,
          height: `${itemHeight}px`
        }"
      >
        item: {{ item }}
      </li>
    </ul>
  </div>
</template>

<style scoped></style>
