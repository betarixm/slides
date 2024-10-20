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
  display: flex;
  flex-direction: column;
  justify-content: center;
}

.slidev-layout.leaflet h2 {
  font-size: var(--font-size-2xl);
  margin-bottom: var(--spacing-p);
}

.slidev-layout.leaflet blockquote {
  color: var(--color-light-text-secondary);
  font-size: var(--font-size-xs);
  font-weight: 300;
}
</style>
