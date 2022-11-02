<template>
  <NuxtLayout>
    <NuxtLoadingIndicator />
    <NuxtErrorBoundary>
      <template #error="{ error }">
        <p>An error occurred: {{ error }}</p>
      </template>

      <NuxtPage />
    </NuxtErrorBoundary>
  </NuxtLayout>
</template>
