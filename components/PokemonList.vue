<script setup lang="ts">
const route = useRoute();
const page = ref(Number.parseInt((route.query.page as string) || "1"));
const offset = computed(() => page.value * 3 - 3);

type Pokemon = {
  name: string;
};

const { data, error } = await useFetch("https://pokeapi.co/api/v2/pokemon", {
  params: {
    limit: 3,
    offset: offset,
  },
  watch: [offset],
  key: `pokemon1`,
  transform: (data: { results: Pokemon[] }) => {
    return data.results.map((item) => ({
      name: item.name,
    }));
  },
});

if (error.value) {
  throw createError({
    statusCode: error.value.statusCode,
    statusMessage: error.value.message,
  });
}
</script>

<template>
  <div>
    <p>Pokemon List / useFetch</p>
    <ul>
      <li v-for="(item, index) in data" :key="index">
        {{ item.name }}
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
