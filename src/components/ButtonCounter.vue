<template>
  <button type="button" @click.prevent="increment">
    You clicked me {{ count }} times.
  </button>
</template>

<script setup lang="ts">
import { ref } from 'vue';

const count = ref(0);

const increment = () => {
  count.value += 1;
};
</script>
