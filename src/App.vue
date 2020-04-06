<template>
  <div id="app">
    <Header
      v-if="questions[index] != null"
      :progress='progress'
      :category='categoryText'
      :difficulty='difficulty'
      :score='score'
    />
    <b-container class="col-12 col-md-6 col-lg-5">
      <Menu 
        v-if="!questions[index]" 
        :startQuiz="startQuiz" 
        v-on:changed="changeCategory"
      />
      <QuestionBox
        :currentQuestion="questions[index]"
        :next='nextQuestion'
        :increment='increment'
        :isFinish='isFinish'
        :isShowScore='isShowScore'
        :showScore='showScore'
        :countDown='countDown'
        v-on:submitted='submitted'
        :qnum='index'
      />
      <ScoreBoard 
        :reset="resetQuiz"
        :isShowScore='isShowScore'
        :numCorrect='numCorrect'
        :score='score'
      />
    </b-container>
    
  </div>
</template>

<script>
import Header from './components/Header.vue'
import Menu from './components/Menu.vue'
import QuestionBox from './components/QuestionBox.vue'
import ScoreBoard from './components/ScoreBoard.vue'

export default {
  name: 'App',
  components: {
    Header,
    QuestionBox,
    Menu,
    ScoreBoard
  },
  data(){
    return{
      score: 0,
      isSubmitted: false,
      isFinish: false,
      progress: 0,
      question: null,
      questions: [],
      index: 0,
      numCorrect: 0,
      numTotal: 0,
      category: null,
      difficulty: null,
      categoryText: null,
      isShowScore: false,
      countDown: 0
    }
  },
  watch:{
    questions(newVal){
      if(newVal != 0){
        this.countDown = 200
        this.countDownTimer()
      }
    }
  },
  methods:{
    countDownTimer() {
        if(this.countDown > 0) {

          setTimeout(() => {
              this.countDown -= 5
              this.countDownTimer()
          }, 1000)
        }
    },
    nextQuestion(){
      if(this.index < (this.questions.length - 1)){
        this.index++
      }
      this.isSubmitted = false
      this.countDown = 200
      this.countDownTimer()

    },
    increment(isCorrect){
      if(isCorrect){
        this.numCorrect++
        this.score += this.countDown
      }
      this.numTotal++
    },
    submitted(){
      this.countDown = 0
      this.isSubmitted = true
      this.progress++
      if(this.progress == 10){
        this.isFinish = true
      }
    },
    showScore(){
      this.isShowScore = true
    },
    changeCategory(value){
      this.category = value.category
      this.difficulty = value.difficulty
      this.categoryText = value.categoryText
      // this.type = value.type
    },
    resetQuiz(){
      this.isSubmitted = false
      this.isFinish = false
      this.progress = 0
      this.question = null
      this.questions = 0
      this.index = 0
      this.numCorrect = 0
      this.numTotal = 0
      this.category = null
      this.difficulty = null
      this.isShowScore = false
      this.score = 0
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
  font-family: 'Lato', sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
body {

  background-image: url('assets/bg.jpg');
  background-size: cover;
}
</style>
