<template>
  <div>
    <div class="container">
      <NuxtLink to="/">
        <img alt="Logo" class="container__image" src="/public/logo.png" />
      </NuxtLink>
      <div class="links">
        <VueHeaderLink
          v-for="{ link, text } in links"
          :link="link"
          :text="text"
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
</script>

<style lang="scss" scoped>
@import "/assets/theme-colors.scss";
.container {
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding: 0.5rem 2rem 0 2rem;
  @include backgrondBlur;

  &__image {
    max-height: 50px;
    cursor: pointer;
  }
}

.links {
  display: flex;
  gap: 0.5rem;
}
</style>
