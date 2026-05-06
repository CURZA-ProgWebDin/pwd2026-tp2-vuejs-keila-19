<script setup>
// Recibe el objeto producto por props
defineProps(['producto']);
// Define el evento para avisar al padre que debe borrar
const emit = defineEmits(['remove']);
</script>

<template>
  <tr>
    <td>{{ producto.nombre }}</td>
    <td>${{ producto.precio }}</td>
    <td>{{ producto.stock }} units</td>
    <td>{{ producto.categoria }}</td>
    <td>
      <button @click="emit('remove', producto.id)">Eliminar</button>
    </td>
  </tr>
</template>