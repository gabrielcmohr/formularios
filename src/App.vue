<script setup>
import { reactive, ref } from 'vue'

const titulo = ref('Digite algo...')
const mostrarResultado = ref(false)

const categorias = [

  {
    id:1, nome: "HG"
  },
  {
    id:1, nome: "Minecraft"
  },
  {
    id:1, nome: "Joias"
  },
  {
    id:1, nome: "Vestuario"
  },
  {
    id:1, nome: "Biblioteca"
  },
  {
    id:1, nome: "CS2"
  }

]

const produto = reactive({
  nome: '',
  preco: 0,
  estoque: 0,
  categorias: []
})

function formatarPreco(preco) {
  return `R$ ${preco.toFixed(2).replace(".", ",")}`
}

</script>

<template>
  <h1>{{ titulo }}</h1>
  <div class="container">
    <div class="formulario">
      <h2>Formulario</h2>
      <input type="text" v-model="titulo" />
      <hr />
      <div class="row">
      <label for="">Nome:</label>
      <input type="text" v-model="produto.nome">
    </div>
      <div class="row">
      <label for="">Preço:</label>
      <input type="number" v-model="produto.preco">
    </div>
      <div class="row">
      <label for="">Estoque:</label>
      <input type="number" v-model="produto.estoque">
    </div>
<!--     <div class="row">
      <label for="">Categoria:</label>
      <input type="text" v-model="produto.categorias">
    </div>  --> 
    <fieldset>
  <legend>Categorias:</legend>
  <div v-for="categoria in categorias" :key="categoria.nome">
    <input type="checkbox" v-model="produto.categorias" :value="categoria.nome" /> {{ categoria.nome }}
  </div>
</fieldset>

    <button @click="mostrarResultado = !mostrarResultado">Mostrar resultado</button>
    </div>
    <Transition>
    <div class="resultado" v-if="mostrarResultado == true">
      <h2>Resultado</h2>
      <h3>Dados do produto</h3>
      <p>Nome: {{ produto.nome }}</p>
      <p>Preço: {{ formatarPreco(produto.preco)}}</p>
      <p>Categorias: {{ produto.categorias }}</p>
      <p>Estoque: {{ produto.estoque }}</p>
    </div>
  </Transition>
  </div>
</template>

<style scoped>

.container {
  display: flex;
  flex-direction: row;
  column-gap: 2rem;
  margin-top: 1.5%;
}
.formulario,
.resultado {
  min-height: 80vh;
  width: 48vw;
  border-radius: 10px;
  padding: 10px;
}
.formulario {
  background-color: azure;
}
.resultado {
  background-color: bisque;
}

</style>

