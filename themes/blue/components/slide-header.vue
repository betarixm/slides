<script setup lang="ts">
import type { TocItem } from "@slidev/types";
import { useSlideContext } from "@slidev/client";

const { $page, $nav } = useSlideContext();

const findParentOfCurrentPage = (items: TocItem[]): TocItem | undefined => {
  for (const item of items) {
    if (item.children.some((child) => child.no === $page.value)) {
      return item;
    } else {
      const parent = findParentOfCurrentPage(item.children);
      if (parent) {
        return parent;
      }
    }
  }
  return undefined;
};
</script>

<template>
  <header>
    {{ findParentOfCurrentPage($nav.tocTree)?.title }}
  </header>
</template>

<style>
header {
  font-size: var(--font-size-header);
  font-weight: 300;
  color: var(--color-light-text-secondary);
  margin-bottom: var(--spacing-heading-4);
}
</style>
