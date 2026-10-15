<script setup>
import MagazineCard from "./MagazineCard.vue";

defineProps({
  cards: { type: Array, required: true },
});
</script>

<template>
  <ul class="grid" role="list">
    <li v-for="card in cards" :key="card.id">
      <MagazineCard
        :image="card.image"
        :alt="card.alt"
        :title="card.title"
        :category="card.category"
      />
    </li>
  </ul>
</template>

<style lang="sass" scoped>
@use "../styles/variables" as v
@use "../styles/functions" as f
@use "../styles/mixins" as m

.grid
  display: grid
  grid-template-columns: 1fr
  gap: f.rem(v.$space-l)
  margin: 0
  padding: 0
  list-style: none

  @include m.breakpoint(tablet)
    grid-template-columns: repeat(2, 1fr)

  @include m.breakpoint(desktop)
    grid-template-columns: repeat(3, 1fr)

  @include m.breakpoint(wide)
    grid-template-columns: repeat(4, 1fr)
</style>
