<template>

    <div class="transition duration-300 rounded-xl cursor-pointer text-base select-none shadow-sm  text-center" :class="loading ? disabledStyles : props.disabled ? 'cursor-not-allowed bg-gray-200' :
    variant == 'universal' ? 'border bg-black  hover:bg-opacity-80 text-white border-black' :
    variant == 'primary' ? 'border bg-primary-500  hover:bg-primary-600 text-white border-transparent' :
    variant == 'secondary' ? 'border bg-primary-700  hover:bg-accent2-600 text-primary-800 border-accent2-700' :
    variant == 'outline-light' ? 'border border-white text-white' :
    variant == 'outline-dark' ? 'border border-black' : ''">

        <NuxtLink :to="{name: route, params : props.params, query: query}" :class="[defaultStyles, setButtonSize]"
            v-if="props.type == 'link'">
            <slot />
        </NuxtLink>

        <button type="button" :class="[defaultStyles, setButtonSize ]"
            v-if="props.type == 'action'" :disabled="props.disabled">
            <slot />
        </button>

        <button :class="[defaultStyles, setButtonSize, props.disabled ? disabledStyles : '']"
            @mouseover="$emit('mouseover')" @mouseleave="$emit('mouseleave')" v-if="props.type == 'hover'">
            <slot />
        </button>

        <button :class="[defaultStyles, setButtonSize]" type="submit"
            v-if="props.type == 'submit'" :disabled="props.loading || props.disabled">
            <div class="flex justify-center items-center gap-1">
                <div v-if="props.loading && props.loader_type == 'boxes'">
                    <LoadersSquareBoxes />
                </div>
                <div v-show="props.loading && props.loader_type == 'circle'">
                    <LoadersCircle fill_classes="text-gray-400" />
                </div>
                <p v-if="props.loading"></p>
                <div v-show="!props.loading">
                    <slot />

                </div>
            </div>

        </button>
    </div>

</template>

<script setup lang="ts">


const props = defineProps({
    removePadding: {
        type: Boolean,
        default: false
    },

    size: {
        type: String,
        default: 'base' //small, base, medium, large
    },

    loader_type: {
        type: String,
        default: 'circle' // boxes, circle
    },

    active: {
        type: Boolean,
        default: false
    },

    type: {
        type: String,
        default: 'action' //action, hover, submit, link
    },

    variant: {
        type: String,
        default: 'primary' // primary, secondary, outline-light, outline-dark
    },

    disabled: {
        type: Boolean,
        default: false
    },

    loading: {
        type: Boolean,
        default: false
    },

    route:{
        type: String,
        default: 'index'
    },


    params: {
        type: Object,
    },

    query: {
        type: Object,
    },



})

const defaultStyles = 'w-full h-full bg-transparent border-0 outline-none block disabled:cursor-not-allowed'
const disabledStyles = 'cursor-not-allowed bg-gray-100 text-gray-400'

const small_button_size = 'px-4 py-1 text-xs'
const base_button_size = 'px-6 py-2'
const medium_button_size = 'px-6 py-3'
const large_button_size = 'px-6 py-3.5'

const setButtonSize = props.size == 'small' ? small_button_size : props.size == 'medium' ? medium_button_size : props.size == 'large' ? large_button_size : base_button_size

</script>