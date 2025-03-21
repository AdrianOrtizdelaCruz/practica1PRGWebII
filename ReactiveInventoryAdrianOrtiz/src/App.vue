<template>
  <div id="app">
    <h1>Inventario de Productos</h1>
    <ul>
      <li v-for="(producto, index) in inventario" :key="index">
        <div>
          <strong>{{ producto.nombre }}</strong><br>
          Precio: {{ producto.precio }}<br>
          Stock: {{ producto.stock }}<br>
          Disponible: {{ producto.disponible ? 'Sí' : 'No' }}<br>
          <button @click="reducirStock(producto)">Reducir Stock</button>
          <button @click="aumentarStock(producto)">Aumentar Stock</button>
        </div>
        <hr />
      </li>
    </ul>
  </div>
</template>

<script lang="ts">
import { reactive, watch } from 'vue';

interface Producto {
  nombre: string;
  precio: number;
  stock: number;
  disponible: boolean;
}

export default {
  setup() {
    const inventario = reactive<Producto[]>([
      { nombre: 'Producto A', precio: 100, stock: 5, disponible: true },
      { nombre: 'Producto B', precio: 50, stock: 0, disponible: false },
      { nombre: 'Producto C', precio: 75, stock: 3, disponible: true }
    ]);

    watch(
      () => inventario.map((producto) => producto.stock), // Observamos cambios en stock
      (newStocks, oldStocks) => {
        inventario.forEach((producto, index) => {
          if (newStocks[index] === 0) {
            producto.disponible = false;
          } else if (newStocks[index] > 0) {
            producto.disponible = true;
          }
        });
      },
      { deep: true }
    );

    const reducirStock = (producto: Producto) => {
      if (producto.stock > 0) {
        producto.stock--;
      }
    };

    const aumentarStock = (producto: Producto) => {
      producto.stock++;
    };

    return { inventario, reducirStock, aumentarStock };
  }
};
</script>

<style>

</style>
