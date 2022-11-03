<script setup>
const route = useRoute();

useHead({
  title: `${route.meta.title} - Zitrinos`,
  viewport: "width=device-width, initial-scale=1, maximum-scale=1",
  charset: "utf-8",
  meta: [{ name: "description", content: `${route.meta.title} - Zitrinos` }],
  bodyAttrs: {
    class: "bg-slate-200 h-screen",
  },
});
</script>
<template>
  <div id="dashboard-layout">
    <div class="dashboard-layout__header">
      <HeaderGlobal />
      <div class="container mx-auto pt-7">
        <slot />
      </div>
    </div>
  </div>
</template>
