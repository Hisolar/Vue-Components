<template>
  <div>
    <div
      v-if="openDialog"
      class="flex items-center justify-center z-[99999] bg-gray-900 bg-opacity-50 fixed h-full w-full"
    >
      <div class="bg-slate-200 max-w-xl mx-auto">
        <p class="px-4 py-2">
          Dialog <br />Lorem ipsum dolor sit amet, consectetur adipiscing elit,
          sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.
        </p>
        <button @click="emits('closeDialog')" class="px-4 py-2 bg-slate-300">
          Close Dialog
        </button>
      </div>
    </div>
  </div>
</template>

<script setup>
const props = defineProps({
  openDialog: {
    type: Boolean,
    default: false,
  },
});

const emits = defineEmits(["closeDialog"]);
</script>
