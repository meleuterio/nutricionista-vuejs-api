<template>
  <div id="app">
    <header>
      <strong>Nutri VueJS</strong>
    </header>

    <div v-if="loading">
      <h1>Carregando Página...</h1>
    </div>
    <article v-else v-for="item in nutri" :key="item.id" class="post">
      <strong class="titulo">{{ item.titulo }}</strong>
      <img :src="item.capa" />
      <span class="categoria">Categoria: {{ item.categoria }}</span>
      <p class="subtitulo">{{ item.subtitulo }}</p>
      <a class="botao" href="#">Acessar</a>
    </article>
  </div>
</template>

<script>
import axios from 'axios'

export default {
  name: 'App',
  data() {
    return {
      nutri: [],
      loading: true
    }
  },
  async created() {
    const response = await axios.get('https://sujeitoprogramador.com/rn-api/?api=posts')
    console.log(response)
    this.nutri = response.data
    this.loading = false
  }
}
</script>

<style>
  #app {
    display: flex;
    flex-direction: column;
    width: 100%;
    justify-content: center;
    align-items: center;
  }
  header {
    display: flex;
    justify-content: center;
    align-items: center;
    width: 100%;
    height: 60px;
    font-size: 30px;
    background: #495867;
    color: #F7F7FF;
  }

  .post {
    display: flex;
    flex-direction: column;
    justify-content: center;
    width: 700px;
    background: white;
    border-radius: 7px;
    margin: 8px;
    padding: 10px;
  }

  .titulo {
    font-size: 25px;
    margin: 10px 0px 25px 0px ;
  }

  .categoria {
    padding-top: 15px;
    font-weight: bold;
  }

  .botao {
    height: 40px;
    background: none;
    border-radius: 5px;
    border: 2px solid #495867;
    color: #495867;
    display: flex;
    justify-content: center;
    align-items: center;
    text-decoration: none;
    font-size: 18px;
    transition: all 0.5s;
  }

   .botao:hover {
     background: #495867;
     color: white;
   }

</style>
