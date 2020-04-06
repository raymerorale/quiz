<template>
	<div class="question-box-container mt-4" v-if="currentQuestion && !isShowScore">
		
<b-card class="box bg-light shadow">
	<span v-if='!isAnswered' class="float-right h5 p-3 mr-2 redorange"><b>+ {{ countDown }}</b></span>
    <h5 class="text-left m-3 redorange">
		<b>Question {{ qnum + 1 }}</b>
    </h5>
	<b-container class="col-10 question">
		{{ question }}
	</b-container>
    <hr class="my-4 w-75">
    <b-list-group>
		<b-list-group-item
			v-for="(answer, index) in answers"
			:key="index"
			@click="selectedAnswer(index)"
			:class="answerClass(index)"
			:disabled="isAnswered"
			class='choice border rounded-pill w-75'
			>
				{{ answer }}
		</b-list-group-item>
	</b-list-group>
	<b-button href="#" class="m-3 bg-redorange border-0 shadow w" 
		@click="submitAnswer"
		:disabled="selectedIndex === null"
		v-if="!isAnswered"
		>
		Submit
	</b-button>
	<b-button variant="success" href="#" class="m-3 w" 
		@click="next" 
		v-if="isAnswered && !isFinish"
		:disabled='nextDisabled'
		>
		Next
	</b-button>
	<b-button variant="outline-danger" href="#" class="m-3" 
		@click="showScore" 
		v-if="isFinish"
		>
		Finish
	</b-button>

</b-card>
    
    
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
				isAnswered: false,
				nextDisabled: true
			}
		},
		methods:{
			delay(){
				setTimeout(() => {
				this.nextDisabled = false
				}, 1000)
			},
			selectedAnswer(index){
				this.selectedIndex = index
				this.correctIndex = this.answers.indexOf(atob(this.currentQuestion.correct_answer))
			},
			submitAnswer(){
				let isCorrect = false
				if(this.selectedIndex === this.correctIndex){
					isCorrect = true
				}
				this.delay()
				this.isAnswered = true
				this.increment(isCorrect)
				this.$emit('submitted')
			},
			answerClass(index){
				let answerClass = ''
				if(!this.isAnswered && this.selectedIndex === index)
					answerClass = 'bg-redorange text-light'
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
					this.isAnswered = false,
					this.nextDisabled = true
				}
			},
		},
		props:{
			currentQuestion: Object,
			next: Function,
			increment: Function,
			isFinish: Boolean,
			reset: Function,
			isShowScore: Boolean,
			showScore: Function,
			countDown: Number,
			qnum: Number
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
.choice{
	margin: 4px auto 4px auto;
	padding: 6px;
	font-size: 15px;
}
.question{
	font-size: 17px;
	margin-top: 1.75em;
}
.redorange{
	color: #f3533b !important;
}
.bg-redorange{
	background: #f3533b !important;
}
.w{
	width: 5em;
}
</style>
