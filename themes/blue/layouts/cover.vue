<script setup lang="ts">
import SlideFooter from "../components/slide-footer.vue";
</script>

<template>
  <div class="slidev-layout cover">
    <slot />
    <slide-footer />
  </div>
</template>

<style lang="css">
.slidev-layout.cover {
  display: grid;
  grid-template-columns: repeat(12, 1fr);
  grid-template-rows: 4fr 2fr 1fr;
  font-size: var(--font-size-xs);
  font-weight: 150;
}

.slidev-layout.cover h1 {
  align-self: self-end;
  grid-column: span 12;
  font-size: var(--font-size-3xl);
  margin-bottom: var(--spacing-li-base);
}

.slidev-layout.cover blockquote {
  grid-column: span 10;
  margin: 0;
  font-size: var(--font-size-xs);
  color: var(--color-light-text-secondary);
}

.slidev-layout.cover ul {
  display: contents;
  list-style-type: none;
  font-weight: 150;
  font-size: var(--font-size-xs);
}

.slidev-layout.cover ul li {
  grid-column: span 4;
  margin: 0;
  color: var(--color-light-text-secondary);
  font-weight: 150;
}
</style>
