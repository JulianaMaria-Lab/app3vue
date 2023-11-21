<script setup lang="ts">
 import { computed, onMounted, ref } from 'vue';
 import axios from 'axios';
 
  const id = ref("");
  const descricao = ref("");
  const dataHoraLimite = ref("");
  const observacoes = ref("Sem Observações");
  const entregas = ref();
  const buscar = ref()

 async function listarEntregas() {
    entregas.value = (await axios.get("entrega")).data;
  }

  onMounted(() => {
    listarEntregas();
  });


</script>

<template>
  <h1></h1>
  <h2>Buscar Entrega - Data Limite</h2>
  <label>Buscar</label>
  <p><input type="datetime-local"  /></p>
  <br>

    <input type="text" v-model="buscar" placeholder="Data/Hora Limite"/>
        <label>Buscar Entrega por Data/Hora Limite:</label>
  
  <table>
      <thead color="#ffffff">
        <td>ID</td>
        <td>Descrição</td>
        <td>Data/Hora Limite</td>
        <td>Observações</td>
      </thead>
      <tbody>
        <tr v-for="entrega in entregas" :key="entrega.id" >
          <td>{{ entrega.id }}</td>
          <td>{{ entrega.descricao }}</td>
          <td>{{ entrega.dataHoraLimite }}</td>
          <td v-if="entrega.observacoes === null" >{{observacoes }}</td>
          <td v-else >{{ entrega.observacoes }}</td>
        </tr>
      </tbody>
    </table>
 <br>
</template>