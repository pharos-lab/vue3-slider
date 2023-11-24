<template>
    <section class="pl-slider" ref="carousel">
      <slot class="test"></slot>
      <div
        class="pl-slider-prev-item"
        v-show="currentItem != 0"
        @click="prev"
      >
        <ChevronLeftIcon></ChevronLeftIcon>
      </div>
      <div
        class="pl-slider-next-item"
        v-if="slideLeft != 0"
        @click="next"
      >
        <ChevronRightIcon></ChevronRightIcon>
      </div>
    </section>
</template>
  
<script setup>
import { ChevronRightIcon, ChevronLeftIcon } from '@heroicons/vue/24/outline';
import { computed, provide, ref, useSlots } from 'vue';

const props = defineProps({
color: {
    type: String,
    default: 'gray',
    validator(value) {
    // The value must match one of these strings
        return ['gray', 'red', 'orange', 'yellow', 'green', 'blue'].includes(value);
    },
},
visibleItems: {
    type: Number,
    default: 5,
},
});

const currentItem = ref(0);
const carousel = ref('carousel');
const slots = useSlots().default();

const slideLeft = computed(() => {
    return slots.length - props.visibleItems - currentItem.value;
});

provide('currentItem', currentItem);
provide('slideLeft', slideLeft);

function next() {
    currentItem.value++;
}

function prev() {
    currentItem.value--;
}
</script>

<style scoped>
.pl-slider {
    display: flex;
    gap: 16px;
    height: 100px;
    background-color: aquamarine;
    overflow: hidden;
    position: relative;
}

.pl-slider-prev-item, .pl-slider-next-item {
    height: 100%;
    background-color: rgba(0,0,0,.5);
    width: 40px;
    position: absolute;
    display: flex;
    justify-content: center;
    align-items: center;
    color: white;
}

.pl-slider-prev-item {
    left: 0;
}
.pl-slider-next-item {
    right: 0;
}
</style>
  