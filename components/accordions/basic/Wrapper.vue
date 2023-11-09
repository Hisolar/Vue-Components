<script setup lang="ts">

import { ref, provide } from 'vue'

const props = defineProps({
    allowMultiple: {
        type: Boolean,
        default: false
    },

    firstItemActive: {
        type: Boolean,
        default: false,
    }
});

const Items = ref([])

provide('Items', Items.value)
provide('allowMultiple', props.allowMultiple)

</script>

<template>
    <ul class="accordion w-full" role="list" aria-roledescription="accordion">
        <slot></slot>
    </ul>
</template>


<style lang="scss" scoped>
.accordion {
    list-style: none;
    margin: 0;
    padding: 0;

    &__item:last-child {
        border-bottom: none;
    }
}
</style>