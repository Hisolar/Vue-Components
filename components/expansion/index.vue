<template>
  <div>
    <button >Title</button>
  </div>
</template>

<script setup>
const props = defineProps({
  openIt: {
    type: Boolean,
    default: false,
  },
});
</script>
