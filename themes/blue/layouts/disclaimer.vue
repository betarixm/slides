<template>
  <div class="slidev-layout disclaimer">
    <slot />
  </div>
</template>

<style lang="css">
.slidev-layout.disclaimer {
  display: flex;
  flex-direction: column;
  font-size: var(--font-size-2xs);
  padding-bottom: var(--spacing-padding-section-y);
  font-weight: 150;
  background-color: var(--color-light-text-highlight);
  color: var(--color-light-background-base);
}

.slidev-layout.disclaimer h1 {
  margin-bottom: var(--spacing-heading-4);
  grid-column: 1 / 4;
  color: var(--color-light-background-base);
  font-size: var(--font-size-lg);
  margin-bottom: 0.3rem;
}

.slidev-layout.disclaimer blockquote {
  margin-bottom: var(--spacing-heading-4);
  grid-column: 1 / 4;
  flex-grow: 1;

  color: var(--color-light-background-base);
  font-size: var(--font-size-xs);
  font-weight: 150;
}

.slidev-layout.disclaimer img {
  height: 80px;
}

.slidev-layout.disclaimer p:last-of-type {
  margin-bottom: calc(var(--spacing-padding-section-y) / 1.5);
}

.slidev-layout.disclaimer > ul {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  margin: 0 0 0 calc(var(--spacing-padding-section-y) / 1.5);
  padding: calc(var(--spacing-padding-section-y) / 1.5) 0 0 0;
  border-top: solid 1px var(--color-light-background-base);
}

.slidev-layout.disclaimer > ul > li {
  grid-column: span 1;
  margin: 0;
  font-size: var(--font-size-2xs);
}

.slidev-layout.disclaimer ul {
  list-style-type: none;
  margin: 0;
  padding-left: 0;
}

.slidev-layout.disclaimer li {
  font-weight: 150;
  font-size: var(--font-size-2xs);
}

.slidev-layout.disclaimer a {
  color: var(--color-light-background-base);
}
</style>
