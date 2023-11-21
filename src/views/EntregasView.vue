<script setup lang="ts">
  import { onMounted, ref } from 'vue';
  import axios from 'axios';
  import ListEntregas from '../components/ListEntregas.vue'

  const erro = ref("");
  const descricao = ref("");
  const dataHoraLimite = ref("");
  const observacoes = ref(null);
  const peso = ref('');
  const entregas = ref();

async function cadastrar() {
    erro.value = "";
    try{
      await axios.post("entrega", 
        {
          descricao: descricao.value,
          dataHoraLimite: dataHoraLimite.value,
          peso: peso.value,
          observacoes: observacoes.value
        });
    }
    catch(e) {
      erro.value = (e as Error).message;
    }
    buscarEntregas();
    clearModel();
    location.reload();
  }

  async function buscarEntregas() {
    entregas.value = (await axios.get("entrega")).data;
  }

  async function clearModel() {
          descricao.value ='',
          dataHoraLimite.value = '',
          peso.value = '',
          observacoes.value = null
    
  }

  onMounted(() => {
    buscarEntregas();
  });
</script>

<template>
    <div class="about">
    <h1>Entregas</h1>
    <ListEntregas/>

    <div class="about">
        <h2>Cadastrar nova Entrega</h2>
        <p><label>Descrição</label></p>
        <p><input type="text" v-model="descricao"/></p>
        <p><label>Data/Hora Limite</label></p>
        <p><input type="datetime-local" v-model="dataHoraLimite"/></p>
        <p><label>Peso</label></p>
        <p><input type="number" v-model="peso"/></p>
        <p><label>Observações</label></p>
        <p><input type="text" v-model="observacoes"/></p>

        <button type="submit" @click="cadastrar">cadastrar</button>
        <p>{{ erro }}</p>
    </div>
    <div>

    </div>
</div>
</template>