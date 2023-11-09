<script setup lang="ts">

import { ref, inject, computed, onMounted } from 'vue'

const props = defineProps({
    disabled: {
        default: false,
        type: Boolean,
    },

    active: {
        default: false,
        type: Boolean,
    },
});


</script>

<template>
    <div class="w-full py-2 flex items-center justify-between select-none"
        :class="[props.active ? '' : '']">

        <div class="" :class="[disabled ? 'opacity-40 cursor-not-allowed' : '', props.active ? 'font-bold' : '']">
            <slot></slot>
        </div>

        <div class="w-3">
            <IconsChevronDown class="transition duration-300" :class="props.active ? 'transform -rotate-180' : ''" />

        </div>
    </div>
</template>