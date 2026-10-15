<script setup>
import { computed, ref } from "vue";
import MagazineGrid from "./components/MagazineGrid.vue";
import cards from "./data/cards.json";

const categories = ["All", ...new Set(cards.map((card) => card.category))];
const activeCategory = ref("All");

const filteredCards = computed(() =>
  activeCategory.value === "All"
    ? cards
    : cards.filter((card) => card.category === activeCategory.value),
);
</script>

<template>
  <div class="page">
    <header class="masthead">
      <h1 class="masthead__title">Pagefold</h1>
      <p class="masthead__tagline">
        Photo stories from places worth slowing down for.
      </p>
    </header>

    <main>
      <div class="filter" role="group" aria-labelledby="filter-label">
        <span id="filter-label" class="filter__label">Show:</span>
        <button
          v-for="category in categories"
          :key="category"
          type="button"
          class="filter__button"
          :class="{ 'filter__button--active': category === activeCategory }"
          :aria-pressed="category === activeCategory"
          @click="activeCategory = category"
        >
          {{ category }}
        </button>
      </div>

      <p class="results" aria-live="polite">
        Showing {{ filteredCards.length }} of {{ cards.length }} stories
      </p>

      <MagazineGrid :cards="filteredCards" />
    </main>
  </div>
</template>

<style lang="sass" scoped>
@use "./styles/variables" as v
@use "./styles/functions" as f
@use "./styles/mixins" as m

.masthead
  margin-bottom: f.rem(v.$space-l)
  padding-bottom: f.rem(v.$space-m)
  border-bottom: f.rem(3px) solid v.$color-ink

.masthead__title
  font-size: f.rem(40px)
  letter-spacing: -0.02em

  @include m.breakpoint(tablet)
    font-size: f.rem(56px)

.masthead__tagline
  margin-top: f.rem(v.$space-xs)
  color: v.$color-muted

.filter
  display: flex
  flex-wrap: wrap
  align-items: center
  gap: f.rem(v.$space-s)

.filter__label
  font-weight: 700

.filter__button
  min-height: f.rem(44px)
  padding: f.rem(v.$space-s) f.rem(v.$space-m)
  border: f.rem(2px) solid v.$color-ink
  border-radius: f.rem(999px)
  font: inherit
  color: v.$color-ink
  background-color: transparent
  cursor: pointer

  &:hover
    background-color: v.$color-surface

  &--active, &--active:hover
    color: v.$color-surface
    background-color: v.$color-ink

.results
  margin: f.rem(v.$space-m) 0
  color: v.$color-muted
</style>
