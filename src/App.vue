<template>
  <div id="app">
    <img alt="Vue logo" src="./assets/logo.png">
    <h1>{{title.toUpperCase() || 'o title está vazio'}}</h1>
    <p>
      <input type="text" v-model="novoAluno" @keyup.enter="!nomeRepetido ? addAluno():''">
      <button @click="addAluno()" :disabled="nomeRepetido">add aluno</button>
    </p>
    <p type="counter">Quantidade de alunos presentes: {{totalAlunosPresentes}}</p>
    <strong>Estão Gostando?</strong>
    <label :style="gostando == 'sim' ? 'text-decoration: underline':''"><input type="radio" v-model="gostando" value="sim">SIM</label>
    <label :style="gostando == 'nao' ? 'text-decoration: underline':''"><input type="radio" v-model="gostando" value="nao">NÃO</label>
    <p>
      <strong> Alunos presentes: </strong>
      <label v-for="(aluno, index) in alunos"  :key="index">
        <input  type="checkbox" v-model="presentes" :value="aluno">
        {{aluno}}
      </label>
    </p>
    <div v-if="totalAlunosPresentes > 1">
      <strong><p>Oba! se tem mais de um aluno tem sorteio!</p></strong>
      <button @click="sortear()">sortear</button>
      <h1 v-if="sorteado">Parabéns {{sorteado.toUpperCase()}} você ganhou a parte DOIS do workshop! VEM YURI!!!</h1>
    </div>
    <div v-else>
      <h1>Poxa, com menos de 2 alunos não tem sorteio </h1>
    </div>
  </div>
</template>

<script>

export default {
  name: 'App',
  computed: {
    totalAlunosPresentes() {
      return this.presentes.length
    },
    totalCaracteres() {
      return this.novoAluno.length
    }
  },
  watch: {
    novoAluno: function (nome) {
      this.nomeRepetido = this.alunos.indexOf(nome) >= 0 ? true : false
    }
  },
  data() {
    return {
      title: 'Workshop VueJS',
      gostando: 'nao',
      presentes: [],
      alunos: ['DJ','Yuri','Antonio'],
      novoAluno: '',
      nomeRepetido: false,
      sorteado: ''
    }
  },
  methods: {
    addAluno: function () {
      this.alunos.push(this.novoAluno)
      this.novoAluno = ''
    },
    sortear: function () {
      this.sorteado = this.presentes[Math.floor(Math.random()*this.presentes.length)];
    }
  },
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
