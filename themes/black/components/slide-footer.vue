<script setup lang="ts">
import WordmarkPostech from "./wordmark-postech.vue";
import { useNav, useSlideContext } from "@slidev/client";

const { $slidev } = useSlideContext();
const { currentPage, total, currentLayout } = useNav();
</script>

<template>
  <footer>
    <span class="text-left">
      <wordmark-postech style="height: 16px; margin-top: 4px" />
    </span>
    <span class="text-center">
      <template v-if="currentLayout != 'cover'">{{
        $slidev.configs.title
      }}</template>
    </span>
    <span class="text-right">
      <template v-if="currentLayout != 'cover'"
        >{{ currentPage }} / {{ total }}</template
      >
    </span>
  </footer>
</template>

<style>
footer {
  position: absolute;
  bottom: 0;
  padding: var(--spacing-padding-footer-y) var(--spacing-padding-footer-x);
  width: 100%;
  left: 0;
  box-sizing: border-box;
  display: grid;
  grid-template-columns: 1fr 4fr 1fr;
  font-size: var(--font-size-footer);
  font-weight: 300;
  color: var(--color-light-text-secondary);
  line-height: 1;
  border-top: solid 1px var(--color-dark-background-base);
}
</style>
