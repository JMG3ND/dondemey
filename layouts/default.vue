<template>
  <div>
    <VueSkeleton>
      <template #header>
        <ContentHeader />
      </template>
      <template #aside>
        <ContentAside />
      </template>
      <slot/>
    </VueSkeleton>
  </div>
</template>