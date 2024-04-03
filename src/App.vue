<script setup>
import { reactive, ref } from 'vue'
const titulo = ref('Oi VueJs!')
const mostrarResultado = ref(false)

const categorias = [
  {
    id: 1,
    nome: 'Eletrônico'
  },

  {
    id: 2,
    nome: 'Vestuário'
  },

  {
    id: 3,
    nome: 'Brinquedos'
  },

  {
    id: 4,
    nome: 'Beleza'
  }
]
const produto = reactive({
  nome: '',
  preço: 0,
  quantidade: 0,
  categorias: []
})

function formatarPreco(preço) {
  return `R$ ${preço.toFixed(2).replace('.', ',')}` //template string
}
</script>

<template>
  <h1>{{ titulo }}</h1>
  <div class="container">
    <div class="formulario">
      <h2>formulário</h2>
      <input type="text" v-model="titulo" />
      <h3>Informar dados do produto</h3>
      <div class="row">
        <label for="">Nome:</label>
        <input type="text" v-model="produto.nome" />
      </div>

      <div class="row">
        <label for=""> Preço (em reais): </label>
        <input type="number" step="0.01" v-model="produto.preço" />
      </div>

      <div class="row">
        <label for=""> Quantidade: </label>
        <input type="text" v-model="produto.quantidade" />
      </div>

      <fieldset>
        <legend>Categorias</legend>
        <div class="itens-checkbox">
          <template v-for="categoria in categorias" :key="categoria.id">
            <input type="checkbox" :value="categoria.id" v-model="produto.categorias" />
            {{ categoria.nome }}
          </template>
        </div>
      </fieldset>
      <div class="row">
        <label for=""> Categoria: </label>
        <input type="text" v-model="produto.categorias" />
      </div>
      <button @click="mostrarResultado = !mostrarResultado">Mostrar</button>
    </div>

    <div v-if="mostrarResultado" class="resultado">
      <h2>Dados do produto</h2>
      <p>nome: {{ produto.nome }}</p>
      <P>preço: {{ formatarPreco(produto.preço) }}</P>
      <p>em estoque: {{ produto.quantidade }}</p>
      <p>categorias: {{ produto.categorias }}</p>
      <p>{{ mostrarResultado }}</p>
    </div>
  </div>
</template>

<style scoped>
.formulario {
  background-color: pink;
}

.resultado {
  background-color: burlywood;
}

.container {
  display: flex;
  gap: 2rem;
  justify-content: center;
  margin-top: 1rem;
}

.formulario .itens-checkbox {
  display: grid;
  grid-template-columns: auto 1fr;
  align-items: center;
}
.formulario,
.resultado {
  width: 45vw;
  min-height: 70vh;
  border-radius: 20px;
  padding: 20px;
}

.formulario .row {
  margin: 1.3rem 0;
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  width: 80%;
}
</style>
