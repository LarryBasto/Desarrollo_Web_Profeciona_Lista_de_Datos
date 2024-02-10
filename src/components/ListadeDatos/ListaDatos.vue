<template>
    <div>
      <h1>Lista de Datos Generados</h1>
      <button @click="toggleSort">Toggle Sort</button>
      <ul>
        <item-lista-datos v-for="item in items" :key="item.id" :item="item" @change-color="changeColor"></item-lista-datos>
      </ul>
      <div>
        <input type="text" v-model="newItemText" placeholder="Nuevo dato">
        <input type="color" v-model="newItemColor">
        <button @click="addItem">Agregar Dato</button>
      </div>
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

const changeColor = (id: number, newColor: string) => {
  const itemIndex = items.value.findIndex(item => item.id === id);
  if (itemIndex !== -1) {
    items.value[itemIndex].color = newColor;
  }
};
</script>

<style scoped> </style>