<template>
  <div>
    <VueSkeleton>
      <template #header>
        <ContentHeader />
      </template>
      <slot />
    </VueSkeleton>
  </div>
</template>
