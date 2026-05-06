<script setup>
import { ref, computed } from 'vue';
import ProductItem from './ProductItem.vue';

const props = defineProps(['productos']);
const emit = defineEmits(['delete-product']);

const filtroCategoria = ref('Todas');

// Lógica para filtrar los productos según la categoría seleccionada
const productosFiltrados = computed(() => {
  if (filtroCategoria.value === 'Todas') return props.productos;
  return props.productos.filter(p => p.categoria === filtroCategoria.value);
});
</script>

<template>
  <div class="list-container">
    <h3>Lista de Productos</h3>
    
    <label>Filtrar por categoría: </label>
    <select v-model="filtroCategoria">
      <option value="Todas">Todas</option>
      <option value="Electrónica">Electrónica</option>
      <option value="Hogar">Hogar</option>
      <option value="Alimentos">Alimentos</option>
    </select>

    <table border="1" style="width: 100%; margin-top: 10px;" v-if="productosFiltrados.length > 0">
      <thead>
        <tr>
          <th>Nombre</th>
          <th>Precio</th>
          <th>Existencias</th>
          <th>Categoría</th>
          <th>Acción</th>
        </tr>
      </thead>
      <tbody>
        <ProductItem 
          v-for="prod in productosFiltrados" 
          :key="prod.id" 
          :producto="prod" 
          @remove="id => emit('delete-product', id)"
        />
      </tbody>
    </table>
    <p v-else>No hay productos registrados en esta categoría.</p>
  </div>
</template>