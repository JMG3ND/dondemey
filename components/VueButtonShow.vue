<template>
  <div>
    <button
      type="button"
      title="Expandir menú"
      class="button"
      @click="$emit('eventClick')"
    >
      <span class="linea" />
    </button>
  </div>
</template>

<script lang="ts" setup>
defineProps({
  active: Boolean
})
defineEmits(["eventClick"]);
</script>

<style scoped lang="scss">
  @mixin brotherLine {
    content: "";
    display: block;
    position: absolute;
    width: 100%;
    height: 100%;
    background-color: black;
  }

.button {
  background-color: transparent;
  border: none;
  width: 40px;
  height: 30px;
  padding: 2px;
}

.linea {
  display: block;
  position: relative;
  width: 100%;
  height: 4px;
  background-color: black;

  &::after {
    @include brotherLine();
    top: -200%;
  }

  &::before {
    @include brotherLine();
    bottom: -200%;
  }
}
</style>
