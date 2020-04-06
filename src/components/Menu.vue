<template>
	<b-form class="bg-light p-4 rounded-lg shadow form">
		<img src='../assets/quizbox-logo.png' class="img">
		<b-form-group 
			class="text-left font-weight-bold select"
			label="Select Category:" 
			label-for="category">

			<b-form-select
				class="rounded-pill pl-4"
				id="category"
				v-model="category" 
				>
				<b-form-select-option v-for="category in categories" 
					v-bind:value="{ id: category.id, text: category.text }"
					:key="category.id"
				>
				{{ category.text }}
				</b-form-select-option>
			</b-form-select>

		</b-form-group>

		<b-form-group 
			class="text-left font-weight-bold select"
			label="Select Difficulty:" 
			label-for="difficulty">
			
			<b-form-select
				class="rounded-pill pl-4"
				id="difficulty"
				v-model="difficulty" 
				:options="difficultyOptions">
			</b-form-select>

		</b-form-group>
		<!-- <b-form-select 
			v-model="type" 
			:options="typeOptions">
		</b-form-select> -->

		<b-button
			v-if="!clicked"
			:disabled="!isCategory || !isDifficulty"
			class="button font-weight-bold border-0 shadow mt-3 rounded-pill"
			@click="changed(), startQuiz();"
			>START QUIZ!
		</b-button>
		<img class='loader' src='../assets/quizbox-icon.png' v-if="clicked" alt="Loading...">
		<!-- <img class="loader" src="http://i.stack.imgur.com/pC1Tv.jpg" alt="" width="120" height="120"> -->

	</b-form>
</template>
<script>
	export default {
		data() {
			return {
				clicked: false,
				isCategory: false,
				isDifficulty: false,
				category: null,
				difficulty: null,
				// type: null,
				// typeOptions: [
				// 	{ value: null, text: 'Please select an option' },
				// 	{ value: 'multiple', text: 'Multiple Choice' },
				// 	{ value: 'boolean', text: 'True or False' }
				// ],
				difficultyOptions: [
					{ value: null, text: ' ' },
					{ value: 'easy', text: 'Easy' },
					{ value: 'medium', text: 'Average' },
					{ value: 'hard', text: 'Hard' }
				],
				categories: [
					{ id: 9, text: 'General Knowledge' },
					{ id: 10, text: 'Books' },
					{ id: 11, text: 'Film' },
					{ id: 12, text: 'Music' },
					{ id: 13, text: 'Musicals & Theaters' },
					{ id: 14, text: 'Televisions' },
					{ id: 15, text: 'Video Games' },
					{ id: 16, text: 'Board Games' },
					{ id: 17, text: 'Science & Nature' },
					{ id: 18, text: 'Computers' },
					// { value: '19', text: 'Mathematics' },
					{ id: 20, text: 'Mythology' },
					{ id: 21, text: 'Sports' },
					{ id: 22, text: 'Geography' },
					{ id: 23, text: 'History' },
					{ id: 24, text: 'Politics' },
					{ id: 25, text: 'Art' },
					{ id: 26, text: 'Celebrities' },
					{ id: 27, text: 'Animals' },
					{ id: 28, text: 'Vehicles' },
					{ id: 29, text: 'Comics' },
					{ id: 30, text: 'Gadgets' },
					{ id: 31, text: 'Anime & Manga' },
					{ id: 32, text: 'Cartoons' }
				],
				customize: [
					{ category: "" },
					{ difficulty: "" },
					{ categoryText: "" }
					// { type: "" }
				]
			}
		},
		methods:{
			changed(){
				this.customize.category = this.category.id
				this.customize.categoryText = this.category.text
				this.customize.difficulty = this.difficulty
				// this.customize.type = this.type
				this.$emit('changed', this.customize)
				this.clicked = true
			}
			// changed() {
				
			// }
		},
		props:{
			startQuiz: Function
		},
		watch: {
			category: function(newVal){
				if(newVal != null){
					this.isCategory = true		
				}
				else
					this.isCategory = false
			},
			difficulty: function(newVal){
				if(newVal != null){
					this.isDifficulty = true
				}
				else
					this.isDifficulty = false
			}
		}
		
	}
</script>
<style>
	.form{
		margin-top: 18vh;
	}
	.select{
		margin-right: auto;
		margin-left: auto;
		width: 75%;
	}
	.img{
		width: 90%;
	}
	.button{
		background-image: linear-gradient(to right, #f3533b , #fa9f42, #8cd77a, #5bcec9);
	}
	.loader {
    width: 50px !important;
    -webkit-animation:spin 3s linear infinite;
    -moz-animation:spin 3s linear infinite;
    animation:spin 3s linear infinite;
}
@-moz-keyframes spin { 100% { -moz-transform: rotate(360deg); } }
@-webkit-keyframes spin { 100% { -webkit-transform: rotate(360deg); } }
@keyframes spin { 100% { -webkit-transform: rotate(360deg); transform:rotate(360deg); } }
</style>



