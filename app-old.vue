<script setup lang="ts">
import { ref } from 'vue';

// Opciones de datos
const winboxOptions = ref(['Bird Road', 'West Hialeah', 'West Hialeah HLC', 'Kendall', 'East Hialeah 445']);
const fallaOptions = ref(['Reportada', 'Detectada']);
const errorOptions = ref(['Pantalla en blanco', 'Emision Parada', 'Winbox sin internet', 'Streaming pausado']);
const herramientaOptions = ref(['.Net', 'Escritorio remoto', 'Soporte remoto', 'Soporte presencial']);
const clienteOptions = ref(['LeonMC', 'El Country', 'INDC', 'LCC']);
const selectedCliente = ref(clienteOptions.value[0]);

// Datos de las filas
const rows = ref([
  { winbox: '', falla: '', tipoError: '', herramienta: '', fechaReporte: '', fechaSolucion: '', tiempoResolucion: '' },
]);

// Métodos
const addRow = () => {
  rows.value.push({ winbox: '', falla: '', tipoError: '', herramienta: '', fechaReporte: '', fechaSolucion: '', tiempoResolucion: '' });
};

const deleteRow = (index) => {
  rows.value.splice(index, 1);
};

const saveData = () => {
  console.log('Data saved:', rows.value);
  // Aquí puedes añadir lógica para enviar los datos al servidor o guardarlos localmente
};

const changeCliente = (event) => {
  selectedCliente.value = event.target.value;
  // Aquí puedes añadir lógica para cargar datos específicos del cliente seleccionado
  console.log('Cliente cambiado a:', selectedCliente.value);
};
</script>

<template>
  <div class="relative overflow-x-auto shadow-md sm:rounded-lg p-2">
    <div class="flex items-center justify-between flex-col md:flex-row flex-wrap space-y-4 md:space-y-0 py-4 pl-5 bg-white dark:bg-gray-900">
      <label for="table-search" class="sr-only">Search</label>
      <div class="relative">
        <div class="absolute inset-y-0 rtl:inset-r-0 start-0 flex items-center ps-3 pointer-events-none">
          <svg class="w-4 h-4 text-gray-500 dark:text-gray-400" aria-hidden="true" xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 20 20">
            <path stroke="currentColor" stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="m19 19-4-4m0-7A7 7 0 1 1 1 8a7 7 0 0 1 14 0Z"/>
          </svg>
        </div>
        <input type="text" id="table-search-users" class="block pt-2 ps-10 text-sm text-gray-900 border border-gray-300 rounded-lg w-80 bg-gray-50 focus:ring-blue-500 focus:border-blue-500 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500" placeholder="Search for Winbox">
      </div>
      <div class="flex items-center space-x-4">
        <label for="select-cliente" class="text-sm font-medium text-gray-700 dark:text-gray-400">Cliente:</label>
        <select id="select-cliente" v-model="selectedCliente" @change="changeCliente" class="block w-40 mt-1 text-sm dark:text-gray-300 dark:bg-gray-700 border-gray-300 rounded-md focus:ring-blue-500 focus:border-blue-500">
          <option v-for="cliente in clienteOptions" :key="cliente" :value="cliente">{{ cliente }}</option>
        </select>
      </div>
    </div>
    <table class="w-full text-sm text-left rtl:text-right text-gray-500 dark:text-gray-400">
      <thead class="text-xs text-gray-700 uppercase bg-gray-50 dark:bg-gray-700 dark:text-gray-400">
        <tr>
          <th scope="col" class="p-4"></th>
          <th scope="col" class="px-6 py-3">Winbox</th>
          <th scope="col" class="px-6 py-3">Falla</th>
          <th scope="col" class="px-6 py-3">Tipo de error</th>
          <th scope="col" class="px-6 py-3">Herramienta usada</th>
          <th scope="col" class="px-6 py-3">Fecha de reporte</th>
          <th scope="col" class="px-6 py-3">Fecha de solución</th>
          <th scope="col" class="px-6 py-3">Tiempo de resolución</th>
          <th scope="col" class="px-6 py-3">Acciones</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="(row, index) in rows" :key="index" class="bg-white border-b dark:bg-gray-800 dark:border-gray-700 hover:bg-gray-50 dark:hover:bg-gray-600">
          <td class="w-4 p-4"></td>
          <td class="px-6 py-4">
            <select v-model="row.winbox" class="block w-full mt-1 text-sm dark:text-gray-300 dark:bg-gray-700 border-gray-300 rounded-md focus:ring-blue-500 focus:border-blue-500">
              <option v-for="option in winboxOptions" :key="option" :value="option">{{ option }}</option>
            </select>
          </td>
          <td class="px-6 py-4">
            <select v-model="row.falla" class="block w-full mt-1 text-sm dark:text-gray-300 dark:bg-gray-700 border-gray-300 rounded-md focus:ring-blue-500 focus:border-blue-500">
              <option v-for="option in fallaOptions" :key="option" :value="option">{{ option }}</option>
            </select>
          </td>
          <td class="px-6 py-4">
            <select v-model="row.tipoError" class="block w-full mt-1 text-sm dark:text-gray-300 dark:bg-gray-700 border-gray-300 rounded-md focus:ring-blue-500 focus:border-blue-500">
              <option v-for="option in errorOptions" :key="option" :value="option">{{ option }}</option>
            </select>
          </td>
          <td class="px-6 py-4">
            <select v-model="row.herramienta" class="block w-full mt-1 text-sm dark:text-gray-300 dark:bg-gray-700 border-gray-300 rounded-md focus:ring-blue-500 focus:border-blue-500">
              <option v-for="option in herramientaOptions" :key="option" :value="option">{{ option }}</option>
            </select>
          </td>
          <td class="px-6 py-4">
            <input type="date" v-model="row.fechaReporte" class="block w-full mt-1 text-sm dark:text-gray-300 dark:bg-gray-700 border-gray-300 rounded-md focus:ring-blue-500 focus:border-blue-500">
          </td>
          <td class="px-6 py-4">
            <input type="date" v-model="row.fechaSolucion" class="block w-full mt-1 text-sm dark:text-gray-300 dark:bg-gray-700 border-gray-300 rounded-md focus:ring-blue-500 focus:border-blue-500">
          </td>
          <td class="px-6 py-4">
            <input type="text" v-model="row.tiempoResolucion" class="block w-full mt-1 text-sm dark:text-gray-300 dark:bg-gray-700 border-gray-300 rounded-md focus:ring-blue-500 focus:border-blue-500">
          </td>
          <td class="px-6 py-4">
            <button @click="deleteRow(index)" class="text-red-600 hover:text-red-900">Eliminar</button>
          </td>
        </tr>
      </tbody>
    </table>
    <div class="flex justify-end mt-4">
      <button @click="addRow" class="px-4 py-2 bg-green-500 text-white rounded-md">Agregar Fila</button>
      <button @click="saveData" class="ml-2 px-4 py-2 bg-blue-500 text-white rounded-md">Guardar Datos</button>
    </div>
  </div>
</template>

<style scoped>
</style>
