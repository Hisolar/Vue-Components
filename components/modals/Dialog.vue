<script setup lang="ts">

const props = defineProps({
    openDialog: {
        type: Boolean,
        default: false
    },

    position: {
        type: String,
        default: 'right'
    },

    customHeader: {
        type: Boolean,
        default: false
    },

    showFooter: {
        type: Boolean,
        default: false
    },

    showCloseButton: {
        type: Boolean,
        default: true
    },

    showTitle: {
        type: Boolean,
        default: false
    },

    scrollable: {
        type: Boolean,
        default: false
    },

    responsiveClasses: {
        type: String,
    },
});


const emit = defineEmits([
    'continueAction',
    'closeDialog'

])

</script>


<template>
    <div>
        <transition name="fade">
            <div @click="emit('closeDialog')" v-show="openDialog"
                class="h-screen cursor-pointer w-full bg-secondary-900 bg-opacity-80 fixed z-9999">
            </div>
        </transition>

        <transition name="">
            <div class="" v-show="openDialog">
                <div class="fixed px-2 z-9999  -translate-x-1/2 -translate-y-1/2 top-1/2 left-1/2 transform "
                    :class="props.responsiveClasses ? props.responsiveClasses : 'w-full sm:max-w-xl'">
                    <div class="mx-auto relative bg-white rounded-xl">
                        <div v-if="customHeader">
                            <slot name="header"></slot>
                        </div>

                        <div v-else class="w-full relative rounded-lg">
                            <a v-if="props.showCloseButton" @click="emit('closeDialog')"
                                class="z-9999 absolute top-4 right-6 block outline-none border-none px-0 cursor-pointer hover:bg-accent1-100">

                                <div
                                    class="w-10 h-10  shadow-xl hover:scale-75 border-white transition-all duration-300 cursor-pointer p-2 rounded-full flex justify-center items-center bg-white">

                                    <svg width="100%" height="100%" viewBox="0 0 24 24" fill="none"
                                        xmlns="http://www.w3.org/2000/svg">
                                        <path fill-rule="evenodd" clip-rule="evenodd"
                                            d="M19.207 6.207a1 1 0 0 0-1.414-1.414L12 10.586 6.207 4.793a1 1 0 0 0-1.414 1.414L10.586 12l-5.793 5.793a1 1 0 1 0 1.414 1.414L12 13.414l5.793 5.793a1 1 0 0 0 1.414-1.414L13.414 12l5.793-5.793z"
                                            fill="currentColor" />
                                    </svg>
                                </div>

                            </a>

                            <div v-if="props.showTitle"
                                class="z-10 flex justify-center  rounded-xl uppercase font-bold items-center bg-white h-16 text-center px-6 sm:px-12 select-none w-full absolute">
                                <slot name="title" />

                            </div>
                        </div>

                        <div class="py-16 md:py-20">
                            <div class=" px-6 md:px-8 "
                                :class="(props.scrollable ? 'custom-scroll-y max-h-[70vh]' : 'max-h-[70vh] overflow-hidden')">
                                <slot />
                            </div>
                        </div>


                        <div v-if="props.showFooter"
                            class="bg-gray-50 flex items-center  rounded-b-xl absolute overflow-hidden bottom-0 h-16 w-full select-none border-t border-gray-300 dark:border-accent1-500">
                            <div class="w-full px-6 md:px-8">
                                <slot name="footer"></slot>
                            </div>

                        </div>
                    </div>

                </div>
            </div>
        </transition>

    </div>
</template>


