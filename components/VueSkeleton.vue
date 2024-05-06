<template>
  <div>
    <div :style="`padding-top: ${headerHeight}px`" class="skeleton">
      <header ref="header" class="skeleton__header">
        <slot name="header" />
      </header>
      <div class="skeleton__container">
        <aside class="skeleton__aside">
          <div :style="`top: ${headerHeight}px`" class="skeleton__aside__container">
            <slot name="aside" />
          </div>
        </aside>
        <main class="skeleton__main">
          <slot name="main" />
        </main>
      </div>
    </div>
  </div>
</template>

<script setup lang="ts">
//Se obtiene el tamaño del header para ponerlo como padding al esqueleto
const header = ref();
const headerHeight = computed(() =>
  typeof header.value === "object"
    ? header.value.getBoundingClientRect().height
    : 0
);
</script>

<style lang="scss" scoped>
.skeleton {
  &__header {
    z-index: 1;
    position: fixed;
    top: 0;
    left: 0;
    right: 0;
  }
  &__container {
    display: grid;
    grid-template-columns: 1fr 3fr;
  }
  &__aside {
    &__container {
      position: sticky;
    }
  }
}
</style>
