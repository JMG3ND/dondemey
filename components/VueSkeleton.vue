<template>
  <div>
    <div :style="`padding-top: ${headerHeight}px`" class="skeleton">
      <header v-if="$slots.header" ref="header" class="skeleton__header">
        <slot name="header" />
      </header>
      <div
        :class="
          $slots.aside
            ? 'skeleton__container--with-aside'
            : 'skeleton__container'
        "
      >
        <aside v-if="$slots.aside" class="skeleton__aside">
          <div
            :style="`top: ${headerHeight}px`"
            class="skeleton__aside__container"
          >
            <slot name="aside" />
          </div>
        </aside>
        <main class="skeleton__main">
          <slot />
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
  padding-left: 1rem;
  padding-right: 1rem;
  &__header {
    z-index: 1;
    position: fixed;
    top: 0;
    left: 0;
    right: 0;
  }
  &__container {
    &--with-aside {
      display: grid;
      grid-template-columns: 300px 3fr;
      gap: 1rem;
    }
  }
  &__aside {
    &__container {
      position: sticky;
    }
  }
}
</style>
