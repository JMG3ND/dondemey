<template>
  <div>
    <div class="container">
      <img class="container__image" src="/public/logo.png" />
    </div>
  </div>
</template>

<script lang="ts" setup>

</script>

<style lang="scss" scoped>
@import '/assets/theme-colors.scss';
.container {
  padding-left: 2rem;
  padding-top: 0.5rem;
  @include backgrondBlur;

  &__image {
    max-height: 50px;
  }
}
</style>