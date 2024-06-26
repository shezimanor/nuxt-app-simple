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
  }
});
const el = ref(null);
const edgeCount = ref(5);
const scrollTop = ref(0);
const startIndex = ref(0);
const windowHeight = ref(500);
const endIndex = ref(
  Math.min(
    props.list.length - 1,
    Math.floor(windowHeight.value / props.itemHeight) + edgeCount.value
  )
);
useResizeObserver(el, (entries) => {
  console.log('useResizeObserver');
  const entry = entries[0];
  const { height } = entry.contentRect;
  windowHeight.value = height;
  getNewIndex();
});
const itemCount = computed(() => props.list.length);
// 原始長清單的 index 應該要被存在 item 裡面
const virtualList = computed(() =>
  props.list.map((item, index) => Object.assign({ _index: index }, item))
);
// 根據當前的 scrollTop 和 windowHeight 來計算當前顯示的清單
const renderList = computed(() =>
  virtualList.value.slice(startIndex.value, endIndex.value + 1)
);

const onScroll = (e: Event) => {
  const target = e.target as HTMLElement;
  scrollTop.value = target.scrollTop;
  getNewIndex();
};
const getNewIndex = () => {
  startIndex.value = Math.max(
    0,
    Math.floor(scrollTop.value / props.itemHeight) - edgeCount.value
  );
  endIndex.value = Math.min(
    props.list.length - 1,
    Math.floor((scrollTop.value + windowHeight.value) / props.itemHeight) +
      edgeCount.value
  );
};
</script>

<template>
  <div class="v-window" @scroll="onScroll" ref="el">
    <ul
      class="v-list"
      :style="{
        height: `${itemCount * itemHeight}px`
      }"
    >
      <li
        v-for="item in renderList"
        :key="item._index"
        class="v-item"
        :style="{
          transform: `translateY(${item._index * itemHeight}px)`,
          height: `${itemHeight}px`
        }"
      >
        item: {{ item }}
      </li>
    </ul>
  </div>
</template>

<style scoped></style>
