<template>
  <div>
    <div class="skeleton">
      <header ref="header" v-if="$slots.header" class="skeleton__header">
        <slot name="header" />
        <div class="skeleton__showTable">
          <VueButtonShow :active=showAside @event-click="changeShowAside">Tabla de contenido</VueButtonShow>
        </div>
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
            v-if="showAside"
            @click="changeShowAside"
            class="skeleton__aside__panel"
          />
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
//Márgenes del header
//Se hace esto ya que se quiere lograr que haya un márgen de espacio libre
//para que el header tape el contenido de la página
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
const changeShowAside = (): void => {
  showAside.value = !showAside.value;
};
const showAsideClass = computed<string>(() =>
  showAside.value ? "skeleton__aside__container--show" : ""
);
</script>

<style lang="scss" scoped>
@import '/assets/theme-colors';
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
    &__panel {
      display: none;
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
        @include backgrondBlur;
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

      &__panel {
        display: block;
        background-color: rgba(0, 0, 0, 0.3);
        position: fixed;
        top: 0;
        right: 0;
        left: 0;
        bottom: 0;
      }
    }
  }
}
</style>
