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

    hasShadow: {
        default: false,
        type: Boolean
    }
});

const accordion_content = ref() as any

const generateRandomNumber = () => {
    let count = 1;
    return count++;
}

const visible = computed(() => {
    return item.value.active;
})

const item = ref({
    active: false,
}) as any


const Items = inject('Items') as any

const allowMultiple = inject('allowMultiple') as any

const activateFirstItem = async () => {
    if (props.active) {
        item.value.active = true
    }
    return true
}

onMounted(() => {
    activateFirstItem().then(() => {
        Items.push(item.value);
    })
})

const open = () => {
    if (props.disabled) {
        return;
    }

    if (allowMultiple) {

        if (item.value.active === false) {
            item.value.active = true;
            Object.assign({}, ...Items, item.value)
        } else {
            item.value.active = false;
            Object.assign({}, ...Items, item.value)
        }

    } else {

        Items.forEach((item: any) => {
            item.active = false
        });

        item.value.active = true;

        Object.assign({}, ...Items, item.value)
    }
}

const start = () => {
    accordion_content.value.style.height = accordion_content.value.scrollHeight + "px";
}

const end = () => {
    accordion_content.value.style.height = "";
}

</script>


<template>
    <li class="accordion__item w-full px-4 sm:px-6 sm:py-2" :class="[visible ? 'border border-gray-300 rounded-xl bg-white' : '', hasShadow ? 'shadow-lg my-3' : '']">
        <div class="accordion__trigger" :class="{ accordion__trigger_active: visible }" @click="open">
            <!-- This slot will handle the title/header of the accordion and is the part you click on -->
            <slot name="header" :state="{active: visible, disabled: props.disabled}"></slot>
        </div>

        <transition name="accordion" @enter="start" @after-enter="end" @before-leave="start" @after-leave="end">
            <div ref="accordion_content" class="accordion__content w-full" v-show="visible">
                <ul>
                    <!-- This slot will handle all the content that is passed to the accordion -->
                    <slot name="content"></slot>
                </ul>
            </div>
        </transition>
    </li>
</template>

<style scoped lang="scss">
.accordion__item {
    cursor: pointer;
    position: relative;
}

.accordion__trigger {
    display: flex;
    justify-content: space-between;
}

.accordion__content {
    margin: 0;
    padding: 0;

    ul {
        padding: 0;
        margin: 0;
    }
}

.accordion-enter-active,
.accordion-leave-active {
    will-change: height, opacity;
    transition: height 0.3s ease, opacity 0.3s ease;
    overflow: hidden;
}

.accordion-enter-from,
.accordion-leave-to {
    height: 0 !important;
    opacity: 0;
}
</style>