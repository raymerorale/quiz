<template>
	<div v-if='isShowScore'>
		<b-jumbotron class="mt-5">
			<span class="score">{{ score }}</span>
			<h2 v-if="score >= 1500">Passed!</h2>
			<h2 v-else>Failed :(</h2>
			<br>
			<h4>
				You have correctly answered
				<span class="h3">{{ numCorrect }}</span>
				out of <span class="h3">10!</span>
			</h4>
			<b-button variant="warning" href="#" class="m-3" 
				@click="reset" 
				>
				Play Again
			</b-button>
		</b-jumbotron>
	</div>
</template>
<script>
	export default {
		props:{
			numCorrect: Number,
			isShowScore: Boolean,
			reset: Function,
			score: Number
		},
		data(){
			return{
				
			}
		}
	}
</script>
<style>
.score{
	font-size:5em;
}
</style>