<template>
  
  <div>
    <div v-if="dadosCep" class="disp-resultado">
      <p><strong>Logradouro:</strong> {{ dadosCep.logradouro }}</p>
      <p><strong>Bairro:</strong> {{ dadosCep.bairro }}</p>
      <p><strong>Cidade:</strong> {{ dadosCep.localidade }}</p>
      <p><strong>Estado:</strong> {{ dadosCep.uf }}</p>
      <p><strong>Região:</strong> {{ dadosCep.regiao }}</p>
    </div>

    <q-page class="flex justify-center items-center">
      <q-form class="flex column content-center" @submit.prevent="buscarCep">
        <q-input
          v-model="cep"
          label="CEP"
          mask="#####-###" 
          :rules="[val => val.length === 9 || 'CEP inválido']"
        ></q-input>
        <q-btn color="primary" class="q-mt-lg" label="Buscar" type="submit"></q-btn>
      </q-form>
    </q-page>

    
  </div>
</template>

<script setup>
import { ref } from 'vue';

const cep = ref(''); // Modelo para armazenar o CEP digitado
const dadosCep = ref(null); // Modelo para armazenar os dados retornados da API

const buscarCep = async () => {
  // Verifica se o CEP é válido
  if (cep.value.length !== 9) {
    alert('Por favor, insira um CEP válido!');
    return;
  }

  // Realiza a requisição para a API ViaCEP
  try {
    const response = await fetch(`https://viacep.com.br/ws/${cep.value.replace('-', '')}/json/`);
    const data = await response.json();

    if (data.erro) {
      alert('CEP não encontrado!');
    } else {
      dadosCep.value = data; // Preenche os dados na variável
    }
  } catch (error) {
    console.error('Erro ao buscar CEP:', error);
    alert('Ocorreu um erro ao buscar o CEP');
  }
};
</script>

<style scoped>
.disp-resultado {
  margin-top: 20px;
  padding: 10px;
  border: 1px solid #ddd;
  border-radius: 5px;
  background-color: #f9f9f9;
}

q-btn {
  width: 100%;
}
</style>
