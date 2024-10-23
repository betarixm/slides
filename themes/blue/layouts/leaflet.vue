<script setup lang="ts">
import SlideFooter from "../components/slide-footer.vue";
</script>

<template>
  <div class="slidev-layout leaflet">
    <slot />
    <slide-footer />
  </div>
</template>

<style lang="css">
.slidev-layout.leaflet {
  background-color: var(--color-light-text-highlight);
  color: var(--color-light-background-base);
}

.slidev-layout.leaflet h2 {
  color: var(--color-light-background-base);
  font-size: var(--font-size-lg);
  margin-bottom: 0.3rem;
}

.slidev-layout.leaflet blockquote {
  color: var(--color-light-background-base);
  font-size: var(--font-size-xs);
  font-weight: 300;
}
</style>
