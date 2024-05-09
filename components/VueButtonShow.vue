<template>
  <div>
    <button @click="$emit('eventClick')" ></button>
  </div>
</template>

<script lang="ts" setup>
defineEmits(["eventClick"]);
</script>

<style scoped>

</style>
