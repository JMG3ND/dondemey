<template>
  <div>
    <button
      type="button"
      title="Expandir menú"
      class="button"
      :class="active ? 'button-active' : ''"
      @click="$emit('eventClick')"
    >
      <span class="line" />
    </button>
  </div>
</template>

<script lang="ts" setup>
defineProps({
  active: Boolean,
});
defineEmits(["eventClick"]);
</script>

<style scoped lang="scss">
.button {
  background-color: transparent;
  border: none;
  width: 30px;
  height: 30px;
  padding: 2px;

  .line {
    display: block;
    position: relative;
    width: 100%;
    height: 13%;
    background-color: black;
    transition: background-color 0.3s ease-in-out;

    &::after, &::before {
      content: "";
      display: block;
      position: absolute;
      width: 100%;
      height: 100%;
      background-color: black;
      transition: transform 0.3s ease-in-out, rotate 0.3s ease-in-out;
    }
    &::after {
      transform: translateY(-200%);
    }
    &::before {
      transform: translateY(200%);
    }
  }
  &-active {
    .line {
      background-color: transparent;
      &::after,
      &::before {
        background-color: rgb(249, 109, 109);
        top: unset;
        transform: translate(0);
      }
      &::after {
        rotate: 45deg;
      }
      &::before {
        rotate: -45deg;
      }
    }
  }
}
</style>
