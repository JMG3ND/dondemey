<template>
  <div>
    <VueSkeleton>
      <template #header>
        <ContentHeader />
      </template>
      <template #aside>
        <ContentAside />
      </template>
      <NuxtPage />
    </VueSkeleton>
  </div>
  <div></div>
</template>

<style>
/* Estilos de diseño por defecto en la aplicación */
@import url(/assets/defaultstyle.css);
</style>
