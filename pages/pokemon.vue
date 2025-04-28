<script setup lang="ts">
const route = useRoute();

const page = ref(Number.parseInt(route.query.page) || 1);
const offset = computed(() => page.value * 3 - 3);

const { data, error } = await useFetch("https://pokeapi.co/api/v2/pokemon", {
  params: {
    limit: 3,
    offset: offset,
  },
  watch: [offset],
  key: `pokemon1`,
  transform: (data) => {
    return data.results.map((item) => ({
      name: item.name,
    }));
  },
});
</script>

<template>
  <div>
    <h1>Page: pokemo, useFetch</h1>
    <ul>
      <li v-for="(item, index) in data" :key="index">
        {{ item.name }}
      </li>
    </ul>
    <button @click="page--">Prev</button>
    <button @click="page++">Next</button>
    <div>
      <p>page: {{ page }}</p>
      <p>error: {{ error }}</p>
    </div>
  </div>
</template>

<style scoped></style>
