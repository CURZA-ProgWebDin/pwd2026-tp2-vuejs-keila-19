<script setup>
import { reactive } from 'vue';

const emit = defineEmits(['add-product']);

const form = reactive({
  nombre: '',
  precio: 0,
  stock: 0,
  categoria: ''
});

const handleSubmit = () => {
  // Validación básica según la consigna
  if (!form.nombre || !form.categoria || form.precio <= 0 || form.stock < 0) {
    alert("Por favor, completa todos los campos con valores válidos.");
    return;
  }

  // Emitimos el nuevo producto (una copia para no mutar el form)
  emit('add-product', { ...form });

  // Limpiamos el formulario
  form.nombre = '';
  form.precio = 0;
  form.stock = 0;
  form.categoria = '';
};
</script>

<template>
  <div class="form-container">
    <h3>Crear Nuevo Producto</h3>
    <form @submit.prevent="handleSubmit">
      <input v-model="form.nombre" placeholder="Nombre del producto" type="text" /><br>
      <input v-model.number="form.precio" placeholder="Precio" type="number" /><br>
      <input v-model.number="form.stock" placeholder="Existencias" type="number" /><br>
      
      <select v-model="form.categoria">
        <option value="" disabled>Seleccionar Categoría</option>
        <option value="Electrónica">Electrónica</option>
        <option value="Hogar">Hogar</option>
        <option value="Alimentos">Alimentos</option>
      </select><br>
      
      <button type="submit">Guardar Producto</button>
    </form>
  </div>
</template>

<style scoped>
.form-container { margin-bottom: 30px; border: 1px solid #ccc; padding: 15px; }
input, select { margin-bottom: 10px; padding: 5px; width: 100%; max-width: 300px; }
</style>