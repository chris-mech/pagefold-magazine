<script setup>
import MagazineGrid from "./components/MagazineGrid.vue";
import cards from "./data/cards.json";
</script>

<template>
  <main class="page">
    <h1>Pagefold</h1>
    <MagazineGrid :cards="cards" />
  </main>
</template>
