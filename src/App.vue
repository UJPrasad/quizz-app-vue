<template>
  <div id="app">
    <Header :index="index" :correct="correct" :total="total"/>
    <QuestionsBox v-if="questions.length" :question="questions[index]" :next="next" :incrementCorrect="incrementCorrect" :incrementTotal="incrementTotal"/>
    <b-spinner v-else variant="primary" label="Spinning"></b-spinner>
  </div>
</template>

<script>
import Header from './components/Header.vue'
import QuestionsBox from './components/QuestionsBox.vue'

export default {
  name: 'App',
  components: {
    Header,
    QuestionsBox
  },
  data() {
    return {
      questions: [],
      index: 0,
      total: 0,
      correct: 0
    }
  }, 
  methods: {
    next() {
      this.index > 8 ? null : this.index++;
    },
    incrementTotal() {
      this.total++;
    },
    incrementCorrect() {
      this.correct++;
    }
  },
  mounted: function() {
    fetch('https://opentdb.com/api.php?amount=10&category=27&type=multiple')
      .then(res => res.json())
      .then(json => this.questions = json.results)
      .catch(console.log)
  }
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
