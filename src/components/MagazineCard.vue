<script setup>
defineProps({
  image: { type: String, required: true },
  alt: { type: String, required: true },
  title: { type: String, required: true },
  category: { type: String, required: true },
});

const baseUrl = import.meta.env.BASE_URL;
</script>

<template>
  <article class="card">
    <img
      class="card__image"
      :src="`${baseUrl}images/${image}`"
      :alt="alt"
      width="640"
      height="480"
      loading="lazy"
    />
    <div class="card__body">
      <p class="card__category">{{ category }}</p>
      <h2 class="card__title">{{ title }}</h2>
    </div>
  </article>
</template>

<style lang="sass" scoped>
@use "../styles/variables" as v
@use "../styles/functions" as f
@use "../styles/mixins" as m

.card
  @include m.card-surface
  height: 100%

.card__image
  width: 100%
  aspect-ratio: 4 / 3
  object-fit: cover

.card__body
  padding: f.rem(v.$space-m)

  @include m.breakpoint(desktop)
    padding: f.rem(v.$space-l)

.card__category
  margin-bottom: f.rem(v.$space-xs)
  font-size: f.rem(13px)
  font-weight: 700
  letter-spacing: 0.08em
  text-transform: uppercase
  color: v.$color-accent

.card__title
  font-size: f.rem(20px)
</style>
