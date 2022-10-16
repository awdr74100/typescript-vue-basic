<template>
  <button type="button" @click.prevent="increment" :style="{ color: color }">
    You clicked me {{ count }} times.
  </button>
</template>

<script setup lang="ts">
import { ref } from 'vue';

const props = defineProps<{
  color: string;
}>();

const emit = defineEmits<{
  (e: 'updateTotalCount', count: number): void;
}>();

const count = ref(0);

const increment = () => {
  count.value += 1;
  emit('updateTotalCount', 2);
};
</script>
