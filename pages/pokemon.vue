<template>
  <div>
    <h1>Page: pokemon</h1>

    <div style="display: flex; flex-direction: column">
      <NuxtLink to="/pokemon">Go to Pokemon</NuxtLink>
      <NuxtLink to="/pokemon2">Go to Pokemon2</NuxtLink>
    </div>

    <NuxtErrorBoundary>
      <PokemonList />
      <template #error="{ error, clearError }">
        <p>An error occurred: {{ error }}</p>

        <button @click="clearError">Clear error</button>
      </template>
    </NuxtErrorBoundary>
  </div>
</template>
