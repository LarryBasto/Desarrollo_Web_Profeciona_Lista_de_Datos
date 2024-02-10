<template>
    <li class="list-item" :style="{ backgroundColor: item.color }">
      <span class="text" :style="{ color: textColor }">{{ item.text }}</span>
      <button class="btn" @click="changeColor">Cambiar Color</button>
    </li>
  </template>
  
  <script setup lang="ts">
  import { defineProps, ref, onMounted, getCurrentInstance } from 'vue';
  
  interface ListItem {
    id: number;
    text: string;
    color: string;
  }
  
  const props = defineProps<{
    item: ListItem;
  }>();
  
  const ctx = getCurrentInstance();
  const textColor = ref('#000000'); 
  
  const changeColor = () => {
    const newColor = getRandomColor();
    ctx.emit('change-color', props.item.id, newColor);
  };
  
  const getRandomColor = () => {
    return '#' + Math.floor(Math.random() * 16777215).toString(16);
  };
  </script>
  
  <style scoped>
  .list-item {
    padding: 10px;
    margin-bottom: 10px;
    border-radius: 5px;
    display: flex;
    align-items: center;
    transition: background-color 0.3s ease;
  }
  
  .text {
    flex: 1; 
  }
  
  .btn {
    padding: 8px 12px;
    border: none;
    border-radius: 3px;
    background-color: #007bff;
    color: #ffffff;
    cursor: pointer;
    transition: background-color 0.3s ease, transform 0.2s ease;
  }
  
  .btn:hover {
    background-color: #0056b3;
    transform: scale(1.05);
  }
  </style>