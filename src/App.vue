<script setup>
import { ref, computed } from 'vue';
import ProductForm from './components/ProductForm.vue';
import ProductList from './components/ProductList.vue';

// Estado global de la aplicación
const productos = ref([]);

// Lógica de negocio simulada
const crearProducto = (datosProducto) => {
  const nuevo = {
    ...datosProducto,
    id: Date.now() // Generación automática de ID
  };
  productos.value.push(nuevo);
  console.log("Capa de Negocio: Producto creado", nuevo);
};

const eliminarProducto = (id) => {
  productos.value = productos.value.filter(p => p.id !== id);
  console.log("Capa de Negocio: Producto eliminado ID:", id);
};

// Resumen del inventario con computed
const totalProductos = computed(() => productos.value.length);
const valorInventario = computed(() => {
  return productos.value.reduce((acc, p) => acc + (p.precio * p.stock), 0);
});
</script>

<template>
  <div class="main-app">
    <h1>Gestión de Productos - TP2</h1>
    
    <div class="resumen-box">
      <h4>Resumen de Inventario</h4>
      <p>Cantidad total: <strong>{{ totalProductos }}</strong></p>
      <p>Valor total: <strong>${{ valorInventario }}</strong></p>
    </div>

    <ProductForm @add-product="crearProducto" />
    
    <hr />

    <ProductList 
      :productos="productos" 
      @delete-product="eliminarProducto" 
    />
  </div>
</template>

<style>
.main-app { font-family: sans-serif; max-width: 900px; margin: auto; padding: 20px; }
.resumen-box { background: #eef; padding: 10px; border-radius: 5px; margin-bottom: 20px; }
</style>
