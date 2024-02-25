<script lang="ts" setup>
interface Currency {
  id: string;
  name: string;
  symbol: string;
  price_usd: string;
}
const { data } = await useFetch('/api/tickers/?limit=10');
const currentData: any = data.value;
const currencies = ref<Currency[]>(currentData.data);
const columns = [
  {
    key: 'name',
    label: 'Name'
  },
  {
    key: 'symbol',
    label: 'Symbol'
  },
  {
    key: 'price_usd',
    label: 'Price'
  },
  {
    key: 'id',
    label: 'Details'
  }
];
console.log('data', data.value);
</script>

<template>
  <main>
    <h1>Index Page</h1>
    <UTable :rows="currencies" :columns="columns">
      <template #id-data="{ row }">
        <ULink
          :to="`/currency/${row.id}`"
          active-class="text-primary"
          inactive-class="text-primary"
          >Details</ULink
        >
      </template>
    </UTable>
  </main>
</template>

<style scoped></style>
