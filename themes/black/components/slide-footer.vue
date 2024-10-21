<script setup lang="ts">
import { useSlideContext } from "@slidev/client";

const { $slidev, $page, $nav } = useSlideContext();
</script>

<template>
  <footer>
    <template
      v-if="$slidev.themeConfigs.brandImage && $slidev.themeConfigs.brandText"
    >
      <span class="text-left w-[16%]"
        ><img
          :src="$slidev.themeConfigs.brandImage.toString()"
          :alt="$slidev.themeConfigs.brandText.toString()"
          style="height: calc(var(--font-size-footer) - 8px); margin: 4px 0"
      /></span>
    </template>
    <template v-else-if="$slidev.themeConfigs.brandText">
      <span class="text-left w-[16%]">{{
        $slidev.themeConfigs.brandText
      }}</span>
    </template>
    <span
      class="grow-1"
      :class="{
        'text-center': $slidev.themeConfigs.brandText,
        'text-left': !$slidev.themeConfigs.brandText,
      }"
    >
      <template v-if="$nav.currentLayout !== 'cover'">{{
        $slidev.configs.title
      }}</template>
    </span>
    <span class="text-right w-[16%]">
      <template v-if="$nav.currentLayout !== 'cover'"
        >{{ $page }} / {{ $nav.total }}</template
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
  display: flex;
  font-size: var(--font-size-footer);
  font-weight: 300;
  color: var(--color-light-text-secondary);
  line-height: 1;
  border-top: solid 1px var(--color-dark-background-base);
}
</style>
