# 簡單的 Nuxt 專案建立示範

## 初始化 - 利用指令建立專案和檔案

```bash
# 建立專案
npx nuxi@latest init 專案名稱

# 建立 page: index
npx nuxi add page index

# 建立 page: currency/[id].vue
npx nuxi add page "currency/[id]"

# 建立 layout: default
npx nuxi add layout default

# 建立 api
npx nuxi add api "[...]"
```

---

## 1. 改寫 `App.vue`

```html
<template>
  <NuxtLayout>
    <NuxtPage />
  </NuxtLayout>
</template>
```

---

## 2. 編輯 `layput/default.vue`

```html
<template>
  <nav>
    <NuxtLink to="/">Home</NuxtLink>
  </nav>
  <main>
    <slot />
  </main>
</template>
```

---

## 3. 編輯 `server/api/[...].ts`

```javascript
export default defineEventHandler((event) => {
  return $fetch(`https://api.coinlore.net${event.node.req.url}`);
});
```

---

4. 編輯 `page/index.vue`

```html
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
  console.log('data', data.value);
</script>

<template>
  <main>
    <h1>Index Page</h1>
    <table>
      <thead>
        <tr>
          <th>Name</th>
          <th>Symbol</th>
          <th>Price</th>
          <th>Details</th>
        </tr>
      </thead>
      <tr v-for="currency in currencies" :key="currency.id">
        <td>{{ currency.name }}</td>
        <td>{{ currency.symbol }}</td>
        <td>{{ currency.price_usd }}</td>
        <td>
          <NuxtLink :to="`/currency/${currency.id}`"
            >{{ currency.id }}</NuxtLink
          >
        </td>
      </tr>
    </table>
  </main>
</template>

<style scoped></style>
```

## 5. 編輯 `pages/currency/[id].vue`

```html
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
  const coin = coins?.value?.[0];
</script>

<template>
  <div v-if="coin">
    <h2>{{ coin.name }} Detail page</h2>
    <table>
      <thead>
        <th>Symbol</th>
        <th>Rank</th>
        <th>Price - US $</th>
        <th>Market Cap - US $</th>
      </thead>
      <tr>
        <td>{{ coin.symbol }}</td>
        <td>{{ coin.rank }}</td>
        <td>{{ coin.price_usd }}</td>
        <td>{{ coin.market_cap_usd }}</td>
      </tr>
    </table>
  </div>
</template>

<style scoped></style>
```

---

## 6. 安裝 Nuxt UI

後面自由發揮

---
