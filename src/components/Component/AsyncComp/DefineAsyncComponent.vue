<script setup>
import { defineAsyncComponent } from 'vue'
import LoadingComponent from '@/components/Component/AsyncComp/LoadingComponent.vue'

const AsyncComponent = defineAsyncComponent({
  // the loader function
  loader: () =>
    new Promise((resolve) => {
      setTimeout(() => {
        resolve(import('./AsyncComponentA.vue'))
      }, 3000)
    }),

  // A component to use while the async component is loading
  loadingComponent: LoadingComponent,

  // Delay before showing the loading component. Default: 200ms.
  delay: 200,

  // The error component will be displayed if a timeout is
  // provided and exceeded. Default: Infinity.
  timeout: 5000
})
</script>

<template>
  <AsyncComponent />
</template>

<style scoped></style>
