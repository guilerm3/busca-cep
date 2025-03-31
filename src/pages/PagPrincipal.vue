<template>
  
  <div class="flex column flex-center q-mt-xl">
    <div v-if="dadosCep" class="disp-resultado flex column">
      <p><strong>Logradouro:</strong> {{ dadosCep.logradouro }}</p>
      <p><strong>Bairro:</strong> {{ dadosCep.bairro }}</p>
      <p><strong>Cidade:</strong> {{ dadosCep.localidade }}</p>
      <p><strong>Estado:</strong> {{ dadosCep.uf }}</p>
      <p><strong>Região:</strong> {{ dadosCep.regiao }}</p>
    </div>

    <div class=" disp-busca q-mt-xl">
      <q-form class="flex column content-center" @submit.prevent="buscarCep">
        <q-input v-model="cep" label="CEP" mask="#####-###" :rules="[val => val.length === 9 || 'CEP inválido']"/>
        <q-btn color="primary" class="q-mt-lg" label="Buscar" type="submit"></q-btn>
      </q-form>
    </div>

    
  </div>
</template>

<script setup>
import { ref } from 'vue';

const cep = ref('');
const dadosCep = ref(null);

const buscarCep = async () => {
  if (cep.value.length !== 9) {
    alert('Por favor, insira um CEP válido!');
    return;
  }

  try {
    const response = await fetch(`https://viacep.com.br/ws/${cep.value.replace('-', '')}/json/`);
    const data = await response.json();

    if (data.erro) {
      alert('CEP não encontrado!');
    } else {
      dadosCep.value = data;
    }
  } catch (error) {
    console.error('Erro ao buscar CEP:', error);
    alert('Ocorreu um erro ao buscar o CEP');
  }
};
</script>

<style scoped>

.disp-resultado {
  width: 300px;
  margin-top: 20px;
  padding: 10px;
  border: 1px solid #ddd;
  border-radius: 5px;
  background-color: #f9f9f9;
  
  animation: fadeIn 1s ease-out; 
  opacity: 1;
}

.disp-busca {
  width: 300px;
  height: 300px;
  
}

@keyframes fadeIn {
  0% {
    opacity: 0;
    transform: translateY(20px);
  }
  100% {
    opacity: 1;
    transform: translateY(0);
  }
}
</style>
