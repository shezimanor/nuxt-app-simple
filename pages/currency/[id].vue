<script lang="ts" setup>
interface Coin {
  name: string;
  symbol: string;
  rank: number;
  price_usd: string;
  market_cap_usd: string;
}
const route = useRoute();
const { data: coins } = await useFetch<Coin[]>(
  '/api/ticker?id=' + route.params.id
);
const columns = [
  {
    key: 'symbol',
    label: 'Symbol'
  },
  {
    key: 'rank',
    label: 'Rank'
  },
  {
    key: 'price_usd',
    label: 'Price - US $'
  },
  {
    key: 'market_cap_usd',
    label: 'Market Cap - US $'
  }
];
</script>

<template>
  <main>
    <div v-if="coins">
      <h1>{{ coins[0].name }} Detail page</h1>
      <UTable :rows="coins" :columns="columns">
        <template #id-data="{ row }">
          <ULink :to="`/currency/${row.id}`" inactive-class="text-primary"
            >Details</ULink
          >
        </template>
      </UTable>
    </div>
  </main>
</template>

<style scoped></style>
