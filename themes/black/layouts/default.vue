<script setup lang="ts">
import SlideHeader from "../components/slide-header.vue";
import SlideFooter from "../components/slide-footer.vue";
</script>

<template>
  <div class="slidev-layout default">
    <slide-header />
    <slot />
    <slide-footer />
  </div>
</template>

<style lang="css">
.slidev-layout.default h1 {
  margin-bottom: var(--spacing-heading-1);
  font-size: var(--font-size-2xl);
}

.slidev-layout.default h2 {
  margin-bottom: var(--spacing-heading-1);
  font-size: var(--font-size-2xl);
}

.slidev-layout.default h3 {
  margin-bottom: var(--spacing-heading-1);
  font-size: var(--font-size-2xl);
}
</style>
