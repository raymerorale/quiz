<template>
  <div id="app">
    <Header 
      :index='index'
      :numCorrect='numCorrect'
      :numTotal='numTotal'
    />
    
    <b-container>
          <Menu 
            class="col-12 col-md-6 col-lg-5"
            v-if="!questions[index]" 
            :startQuiz="startQuiz" 
            v-on:changed="changeCategory"
          />
          <QuestionBox
            class="col-12 col-md-6 col-lg-5"
            :currentQuestion="questions[index]"
            :next='nextQuestion'
            :increment='increment'
          />
    </b-container>
    
  </div>
</template>

<script>
import Header from './components/Header.vue'
import Menu from './components/Menu.vue'
import QuestionBox from './components/QuestionBox.vue'

export default {
  name: 'App',
  components: {
    Header,
    QuestionBox,
    Menu
  },
  data(){
    return{
      question: null,
      questions: [],
      index: 0,
      numCorrect: 0,
      numTotal: 0,
      category: null,
      difficulty: null
    }
  },
  methods:{
    nextQuestion(){
      if(this.index < (this.questions.length - 1))
      this.index++
    },
    increment(isCorrect){
      if(isCorrect){
        this.numCorrect++
      }
      this.numTotal++
    },
    changeCategory(value){
      this.category = value.category
      this.difficulty = value.difficulty
      // this.type = value.type
    },
    startQuiz(){
      fetch('https://opentdb.com/api.php?amount=10&category=' + this.category + '&difficulty=' + this. difficulty + '&type=multiple&encode=base64', {
      method: 'get'
    })
      .then((response) => {
        return response.json()
      }) 
      .then((jsonData) => {
        this.questions = jsonData.results
      })
    }
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
