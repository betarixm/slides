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
  font-weight: 300;
}

.slidev-layout.disclaimer h1 {
  margin-bottom: var(--spacing-heading-4);
  grid-column: 1 / 4;
  font-size: var(--font-size-lg);
}

.slidev-layout.disclaimer blockquote {
  margin-bottom: var(--spacing-heading-4);
  grid-column: 1 / 4;
  flex-grow: 1;

  font-size: var(--font-size-2xs);
  font-weight: 400;
  color: var(--color-light-text-secondary);
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
  border-top: solid 1px var(--color-dark-background-base);
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
  font-weight: 300;
  font-size: var(--font-size-2xs);
}
</style>
