<template>
	<div class="question-box-container mt-2" v-if="currentQuestion">
		
<b-jumbotron>
 
    <template v-slot:lead>
      {{ question }}
    </template>

    <hr class="my-4">
    <b-list-group>
		<b-list-group-item
			v-for="(answer, index) in answers"
			:key="index"
			@click="selectedAnswer(index)"
			:class="answerClass(index)"
			:disabled="isAnswered"
			>
				{{ answer }}
		</b-list-group-item>
	</b-list-group>
	<b-button variant="primary" href="#" class="m-3" 
		@click="submitAnswer"
		:disabled="selectedIndex === null"
		v-if="!isAnswered"
		>
		Submit
	</b-button>
	<b-button variant="success" href="#" @click="next" class="m-3" v-if="isAnswered">Next</b-button>

</b-jumbotron>
    
    
</div>
	
</template>

<script>
	export default {
		computed:{
			question(){
				return atob(this.currentQuestion.question)
			},
			answers(){
				let answers = [...this.currentQuestion.incorrect_answers]
				answers.push(this.currentQuestion.correct_answer)
				
				for(let i = 0; i < answers.length; i++){
					answers[i] = atob(answers[i])
				}


				for (let i = answers.length - 1; i > 0; i--) {
					const j = Math.floor(Math.random() * (i + 1));
					[answers[i], answers[j]] = [answers[j], answers[i]];
				}
				return answers
			}
		},
		data(){
			return{
				selectedIndex: null,
				correctIndex: null,
				isAnswered: false
			}
		},
		methods:{
			selectedAnswer(index){
				this.selectedIndex = index
				this.correctIndex = this.answers.indexOf(atob(this.currentQuestion.correct_answer))
			},
			submitAnswer(){
				let isCorrect = false
				if(this.selectedIndex === this.correctIndex){
					isCorrect = true
				}
				this.isAnswered = true
				this.increment(isCorrect)
			},
			answerClass(index){
				let answerClass = ''
				if(!this.isAnswered && this.selectedIndex === index)
					answerClass = 'bg-primary text-light'
				else if(this.isAnswered && this.correctIndex === index)
					answerClass = 'bg-success text-light'
				else if(this.isAnswered && this.selectedIndex === index && this.correctIndex !== index)
					answerClass = 'bg-danger text-light'
				return answerClass
			}

			

		},
		watch:{
			currentQuestion: {
				immediate: true,
				handler(){
					this.selectedIndex = null,
					this.isAnswered = false
				}
			}
		},
		props:{
			currentQuestion: Object,
			next:Function,
			increment: Function

		}

	}
</script> 
<style scoped>
.list-group-item:hover{
	background: #EEE;
	cursor: pointer;
}
.question-box-container{
	margin: auto;
}
</style>
