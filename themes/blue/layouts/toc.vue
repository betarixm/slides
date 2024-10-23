<script setup lang="ts">
import SlideFooter from "../components/slide-footer.vue";
</script>

<template>
  <div class="slidev-layout toc">
    <slot />
    <slide-footer />
  </div>
</template>

<style lang="css">
.slidev-layout.toc {
  background-color: var(--color-light-text-highlight);
  color: var(--color-light-background-base);
}

.slidev-layout.toc > ul {
  display: grid;
  height: 100%;
  grid-auto-rows: 1fr;
  padding: 0;
  margin: 0;
  list-style-type: none;
}

.slidev-layout.toc > ul > li {
  border-top: 1px solid var(--color-light-background-base);
  padding: var(--spacing-li-base) 0;
  margin: 0;
  display: grid;
  grid-template-columns: 1fr 1fr;
  font-size: var(--font-size-2xl);
  font-weight: 400;
}

.slidev-layout.toc > ul > li > ul {
  font-size: var(--font-size-xs);
  line-height: 1;
  list-style-type: disc;
  font-weight: 300;
}
</style>
