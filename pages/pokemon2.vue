<script setup lang="ts">
const route = useRoute();

const page = ref(Number.parseInt(route.query.page) || 1);
const offset = computed(() => page.value * 3 - 3);

const { data, error } = await useAsyncData(
  "pokemon2",
  () =>
    $fetch("https://pokeapi.co/api/v2/pokemon", {
      params: {
        limit: 3,
        offset: offset.value,
      },
    }).then((res) => res.results.map((item) => item.name)),
  {
    watch: [offset],
  }
);
</script>

<template>
  <div>
    <h1>Page: pokemo2, useAsyncData</h1>
    <ul>
      <li v-for="(item, index) in data" :key="index">
        {{ item }}
      </li>
    </ul>
    <button @click="page--">Prev</button>
    <button @click="page++">Next</button>
    <div>
      <p>page: {{ page }}</p>
      <p>offset: {{ offset }}</p>
      <p>error: {{ error }}</p>
    </div>
  </div>
</template>

<style scoped></style>
