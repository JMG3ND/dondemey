<template>
  <div>
    <div :style="`padding-top: ${headerHeight}px`" class="skeleton">
      <header
        id="header"
        v-if="$slots.header"
        ref="header"
        class="skeleton__header"
      >
        <slot name="header" />
        <button class="skeleton__showTable" @click="showTable = !showTable">
          Tabla de contenido
        </button>
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
const header = ref<HTMLElement | null>(null);
const headerHeight = computed<Number>(():Number =>
  header.value
    ? header.value?.offsetHeight
    : 0
);

onMounted(() => {
  console.log(header.value)
})

//Variable que oculta y muestra la tabla de contenido en dispositivos móviles
const showTable = ref(false);
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
  &__showTable {
    display: none;
  }
}

@media screen and (max-width: 900px) {
  .skeleton {
    &__showTable {
      display: block;
    }
  }
}
</style>
