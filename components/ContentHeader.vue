<template>
  <div>
    <div class="header">
      <NuxtLink to="/">
        <img alt="Logo" class="header__image" src="/public/logo.png" />
      </NuxtLink>
      <div class="header__links">
        <div class="header__links__container" :class="classShowMenu">
          <VueHeaderLink
            v-for="{ link, text } in links"
            :link="link"
            :text="text"
          />
        </div>
        <VueButtonShow
          :active="showMenu"
          @eventClick="changeShowMenu"
          class="header__links__button-show"
        />
      </div>
    </div>
  </div>
</template>

<script lang="ts" setup>
const links = [
  {
    link: "/",
    text: "Home",
  },
  {
    link: "/example1",
    text: "Ejemplo 1",
  },
  {
    link: "/example2",
    text: "Ejemplo 2",
  },
];

const showMenu = ref<boolean>(false);
const changeShowMenu = () => {
  showMenu.value = !showMenu.value;
};
const classShowMenu = computed(() =>
  showMenu.value ? "header__links__container-show" : ""
);
</script>

<style lang="scss" scoped>
@import "/assets/theme-colors.scss";
.header {
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding: 0.5rem 2rem 0 2rem;
  @include backgrondBlur;

  &__image {
    max-height: 50px;
    cursor: pointer;
  }

  &__links {
    &__container {
      display: flex;
      gap: 0.5rem;
    }
    &__button-show {
      display: none;
    }
  }
}
@media screen and (max-width: 900px) {
  .header__links {
    &__container {
      flex-direction: column;
      padding: 2rem;
      @include backgrondBlur;

      width: 300px;
      height: calc(100vh - var(--6d7d849d-headerHeight));

      position: absolute;
      top: 100%;
      right: 0;
      transform: translateX(100%);
      transition: transform 0.3s ease-in-out;

      &-show {
        transform: translateX(0);
      }
    }
    &__button-show {
      display: block;
    }
  }
}
</style>
