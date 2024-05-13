<template>
  <div>
    <NuxtLink :to="link">
      <div class="link">
        {{ text }}
      </div>
    </NuxtLink>
  </div>
</template>

<script lang="ts" setup>
defineProps({
  link: String,
  text: String,
});
</script>

<style lang="scss" scoped>
@import '/assets/theme-colors';
a {
  text-decoration: none;
}
.link {
  color: white;
  text-decoration: none;
  text-align: center;
  padding: 0.5rem 1rem;
  background-color: $color2;
  border-radius: 10px;
  border-bottom: 4px solid $color7;
  transition: border-bottom 0.1s ease-in-out, margin-top 0.1s ease-in-out;

  .router-link-active &,
  .router-link-exact-active & {
    margin-top: 4px;
    border-bottom: 0px solid $color7;
  }
}
</style>
