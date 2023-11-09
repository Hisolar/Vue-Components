<template>
  <button
    class="px-4 py-2 flex gap-1"
    :class="[
      props.variant == 'elevated'
        ? 'bg-gray-500 rounded-full'
        : props.variant == 'outline'
        ? 'border rounded-full'
        : props.variant == 'text'
        ? ' bg-transparent'
        : props.variant == 'plain'
        ? 'opacity-60 hover:opacity-100'
        : '',
    ]"
  >
    <div v-if="props.prependIcon">
      <slot name="icon"></slot>
    </div>

    <div><slot /></div>

    <div v-if="props.apendIcon">
      <slot name="icon"></slot>
    </div>

    <div v-if="props.closed">
      <slot name="icon"></slot>
    </div>
  </button>
</template>

<script setup>
const props = defineProps({
  variant: {
    type: String,
  },

  prependIcon: {
    type: Boolean,
    default: false,
  },
  apendIcon: {
    type: Boolean,
    default: false,
  },
  closed: {
    type: Boolean,
    default: false,
  },
});
</script>
