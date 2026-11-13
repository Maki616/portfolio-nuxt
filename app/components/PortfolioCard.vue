<script setup>
defineProps({
  title: {
    type: String,
    default: '',
  },
  titleTag: {
    type: String,
    default: 'h2',
  },
  titleClass: {
    type: String,
    default: '',
  },
  bodyClass: {
    type: String,
    default: '',
  },
})
</script>

<template>
  <article class="card portfolio-card border border-base-content/20 bg-base-100/10 shadow-xl backdrop-blur-xl">
    <figure v-if="$slots.media" class="portfolio-card-media">
      <slot name="media" />
    </figure>

    <div class="card-body" :class="bodyClass">
      <component
        :is="titleTag"
        v-if="title"
        class="card-title"
        :class="titleClass"
      >
        {{ title }}
      </component>
      <slot />
    </div>
  </article>
</template>
