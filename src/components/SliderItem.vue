<template>
    <div class="pl-slider-item">
      <slot></slot>
    </div>
</template>

<script setup>
import { computed, inject, getCurrentInstance } from 'vue';

const instance = getCurrentInstance();
const currentItem = inject('currentItem');
const slideLeft = inject('slideLeft');

const size = computed(() => {
    return (instance.parent.refs.carousel.offsetWidth - instance.parent.props.visibleItems * 16) / (instance.parent.props.visibleItems + 0.5);
});

const pixelSize = computed(() => {
    return size.value + 'px';
});

const translateSize = computed(() => {
    if (slideLeft.value == 0) {
        return '-' + (size.value + 16) * (currentItem.value - 0.5) + 'px';
    }
    return '-' + (size.value + 16) * currentItem.value + 'px';
});
</script>

<style>
.pl-slider-item {
    width: v-bind(pixelSize);
    transform: translateX(v-bind(translateSize));
    transition: transform 1s ease;
    flex-shrink: 0;
}
</style>
  