<template>
  <div>
    <div class="skeleton">
      <header
        ref="header"
        v-if="$slots.header"
        class="skeleton__header"
      >
        <slot name="header" />
        <button class="skeleton__showTable" @click="showAside = !showAside">
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
          <div :class="`skeleton__aside__container ${showAsideClass}`">
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
//Margenes del header
const header = ref<HTMLElement | null>(null);
const headerHeight = ref<string>("0px");
const changeHeight = () => {
  headerHeight.value = `${header.value?.offsetHeight}px`;
};
onMounted(() => {
  changeHeight();
  window.addEventListener("resize", changeHeight);
});
onUnmounted(() => window.removeEventListener("resize", changeHeight));

//Lógica del aside
const showAside = ref<boolean>(false);
const showAsideClass = computed<string>(() =>
  showAside.value ? "skeleton__aside__container--show" : ""
);
</script>

<style lang="scss" scoped>
$asideWidth: 300px;

.skeleton {
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
      grid-template-columns: $asideWidth 1fr;
      gap: 1rem;
      padding-top: v-bind(headerHeight);
    }
  }
  &__aside {
    &__container {
      position: sticky;
      top: v-bind(headerHeight);
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
    &__container {
      &--with-aside {
        display: block;
      }
    }
    &__aside {
      &__container {
        background-color: white;
        position: fixed;
        width: $asideWidth;
        left: 0;
        top: v-bind(headerHeight);
        bottom: 0;
        transform: translateX(-100%);
        transition: transform 0.3s ease-in-out;
        &--show {
          transform: translate(0);
        }
      }
    }
  }
}
</style>
