<script lang="ts" setup>
const emit = defineEmits(["update:isOpen"]);

function closeModal() {
  emit("update:isOpen", false);
}

defineProps<{
  isOpen: boolean;
}>();
</script>

<template>
  <div
    v-show="isOpen"
    class="absolute z-50 inset-0 flex items-center justify-center bg-gray-700 bg-opacity-50"
  >
    <div class="modal-box">
      <div class="modal-header flex justify-between">
        <h3 class="modal-title font-bold text-xl">Detalhes</h3>
        <svg
          @click="closeModal"
          xmlns="http://www.w3.org/2000/svg"
          class="w-8 h-8 text-red-500 cursor-pointer"
          fill="none"
          viewBox="0 0 24 24"
          stroke="currentColor"
        >
          <path
            stroke-linecap="round"
            stroke-linejoin="round"
            stroke-width="2"
            d="M10 14l2-2m0 0l2-2m-2 2l-2-2m2 2l2 2m7-2a9 9 0 11-18 0 9 9 0 0118 0z"
          />
        </svg>
      </div>
      <div class="modal-body mt-5">
        <slot />
      </div>
    </div>
  </div>
</template>
