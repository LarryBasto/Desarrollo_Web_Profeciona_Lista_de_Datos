<template>
    <li :style="{ color: item.color, backgroundColor: item.color }">
      {{ item.text }}
      <button @click="changeColor">Cambiar Color</button>
    </li>
  </template>

<script setup lang="ts">
import { defineProps } from 'vue';

interface ListItem {
  id: number;
  text: string;
  color: string;
}

const props = defineProps<{
  item: ListItem;
}>();

const changeColor = () => {
  const newColor = getRandomColor();
  emit('change-color', props.item.id, newColor);
};

const getRandomColor = () => {
  return '#' + Math.floor(Math.random() * 16777215).toString(16);
};
</script>

<style scoped> </style>