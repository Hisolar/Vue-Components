<template>
  <div
    class="px-2 py-1"
    :class="[
      props.variant == 'outline'
        ? 'outline'
        : props.variant == 'tonal'
        ? 'bg-gray-500'
        : 'bg-transparent',

      props.rounded ? 'rounded-xl' : '',
    ]"
  >
    <div v-if="props.loading">
      <div class="horizontal-bar-wrap">
        <div class="bar3 bar"></div>
        <!--   <div class="bar2 bar"></div>
  <div class="bar3 bar"></div>
  <div class="bar4 bar"></div> -->
      </div>
    </div>
    <div v-if="props.showTitle" class="font-bold text-2xl">
      <slot name="title"></slot>
    </div>

    <div v-if="props.showSubTitle">
      <slot name="subtitle"></slot>
    </div>
    <slot> </slot>
    <div>
      <slot name="action"></slot>
    </div>
  </div>
</template>

<script setup>
const props = defineProps({
  variant: {
    type: String,
  },
  showTitle: {
    type: Boolean,
    default: false,
  },
  showSubTitle: {
    type: Boolean,
    default: false,
  },
  loading: {
    type: Boolean,
    default: false,
  },

  rounded: {
    type: Boolean,
    default: false,
  },
});
</script>

<style lang="scss">
@keyframes barWidth {
  0% {
    width: 0%;
  }
  25% {
    width: 50%;
  }
  50% {
    width: 100%;
  }
  75% {
    width: 50%;
  }
  100% {
    width: 0%;
  }
}
@keyframes barWidth2 {
  0% {
    width: 0%;
  }
  50% {
    width: 50%;
  }
  100% {
    width: 100%;
  }
}
.horizontal-bar-wrap {
  height: 4px;
  width: 100%;
  .bar {
    position: relative;
    width: 0%;
    height: 100%;
    margin: 0 auto;
    animation: barWidth;
    animation-duration: 2s;
    animation-iteration-count: infinite;
    animation-timing-function: linear;
    &.bar1 {
      animation-delay: 0s;
      background: #02a09a;
      top: 0;
      z-index: 1;
    }
    &.bar2 {
      animation-delay: 2s;
      background: green;
      top: -4px;
      z-index: 2;
    }
    &.bar3 {
      background: blue;
      top: -8px;
      z-index: 3;
    }
    &.bar4 {
      animation-delay: 6s;
      background: magenta;
      top: -12px;
      z-index: 4;
    }
  }
}
</style>
