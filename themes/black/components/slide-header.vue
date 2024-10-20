<script setup lang="ts">
import type { TocItem } from "@slidev/types";
import { useNav } from "@slidev/client";

const { tocTree, currentPage } = useNav();

const findParentOfCurrentPage = (items: TocItem[]): TocItem | undefined => {
  for (const item of items) {
    if (item.children.some((child) => child.no === currentPage.value)) {
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
    {{ findParentOfCurrentPage(tocTree)?.title }}
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
