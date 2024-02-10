<template>
    <div>
      <h1>Lista de Datos Generados</h1>
      <div class="input-container">
        <input type="text" v-model="newItemText" placeholder="Nuevo dato">
        <input type="color" v-model="newItemColor">
        <button class="btn" @click="addItem">Agregar Dato</button>
        <button class="btn toggle-btn" @click="toggleSort">Ordenar</button>
      </div>
      <ul>
        <item-lista-datos v-for="item in items" :key="item.id" :item="item" @change-color="changeColor" @delete-item="deleteItem"></item-lista-datos>
      </ul>
    </div>
  </template>
  
  <script lang="ts" setup>
  import { ref } from 'vue';
  import ItemListaDatos from './ItemListaDatos.vue';
  
  interface DataItem {
    id: number;
    text: string;
    color: string;
  }
  
  const items = ref<DataItem[]>([]);
  const newItemText = ref('');
  const newItemColor = ref('#ffffff');
  const sortAsc = ref(true);
  
  const addItem = () => {
    if (newItemText.value.trim().length > 0) {
      items.value.push({
        id: Date.now(),
        text: newItemText.value,
        color: newItemColor.value
      });
      newItemText.value = '';
      newItemColor.value = '#ffffff';
    }
  };
  
  const toggleSort = () => {
    sortAsc.value = !sortAsc.value;
    items.value.sort((a, b) => {
      return sortAsc.value ? a.id - b.id : b.id - a.id;
    });
  };
  
  const deleteItem = (id: number) => {
    const index = items.value.findIndex(item => item.id === id);
    if (index !== -1) {
      items.value.splice(index, 1);
    }
  };
  
  const changeColor = (id: number, newColor: string) => {
    const itemIndex = items.value.findIndex(item => item.id === id);
    if (itemIndex !== -1) {
      items.value[itemIndex].color = newColor;
    }
  };
  </script>
  
  <style scoped>
  .input-container {
    margin-bottom: 10px;
  }
  
  .btn {
    padding: 8px 12px;
    margin-right: 10px;
    border: none;
    border-radius: 3px;
    background-color: #007bff;
    color: #ffffff;
    cursor: pointer;
    transition: background-color 0.3s ease, transform 0.2s ease;
  }
  
  .btn.toggle-btn {
    background-color: #28a745;
  }
  
  .btn:hover {
    background-color: #0056b3;
    transform: scale(1.05);
  }
  </style>
  