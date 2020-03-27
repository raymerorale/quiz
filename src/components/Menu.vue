<template>
	<b-form class="border bg-light p-4 mt-5 rounded shadow form">
		<b-form-group 
			class="text-left font-weight-bold"
			label="Select Category:" 
			label-for="category">

			<b-form-select
				id="category"
				v-model="category" 
				:options="categoryOptions">
			</b-form-select>

		</b-form-group>

		<b-form-group 
			class="text-left font-weight-bold"
			label="Select Difficulty:" 
			label-for="difficulty">
			
			<b-form-select 
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
			:disabled="isCategory || isDifficulty"
			class="bg-primary border-0 shadow w-25 mt-2"
			@click="changed(), startQuiz();"
			>Start
		</b-button>
		<b-spinner v-if="clicked" label="Loading..."></b-spinner>

	</b-form>
</template>
<script>
	export default {
		data() {
			return {
				clicked: false,
				isCategory: true,
				isDifficulty: true,
				category: null,
				difficulty: null,
				// type: null,
				// typeOptions: [
				// 	{ value: null, text: 'Please select an option' },
				// 	{ value: 'multiple', text: 'Multiple Choice' },
				// 	{ value: 'boolean', text: 'True or False' }
				// ],
				difficultyOptions: [
					{ value: null, text: 'Difficulty' },
					{ value: 'easy', text: 'Easy' },
					{ value: 'medium', text: 'Average' },
					{ value: 'hard', text: 'Hard' }
				],
				categoryOptions: [
					{ value: null, text: 'Category' },
					{ value: '9', text: 'General Knowledge' },
					{ value: '10', text: 'Books' },
					{ value: '11', text: 'Film' },
					{ value: '12', text: 'Music' },
					{ value: '13', text: 'Musicals & Theaters' },
					{ value: '14', text: 'Televisions' },
					{ value: '15', text: 'Video Games' },
					{ value: '16', text: 'Board Games' },
					{ value: '17', text: 'Science & Nature' },
					{ value: '18', text: 'Computers' },
					// { value: '19', text: 'Mathematics' },
					{ value: '20', text: 'Mythology' },
					{ value: '21', text: 'Sports' },
					{ value: '22', text: 'Geography' },
					{ value: '23', text: 'History' },
					{ value: '24', text: 'Politics' },
					{ value: '25', text: 'Art' },
					{ value: '26', text: 'Celebrities' },
					{ value: '27', text: 'Animals' },
					{ value: '28', text: 'Vehicles' },
					{ value: '29', text: 'Comics' },
					{ value: '30', text: 'Gadgets' },
					{ value: '31', text: 'Anime & Manga' },
					{ value: '32', text: 'Cartoons' }
				],
				customize: [
					{ category: "" },
					{ difficulty: "" },
					// { type: "" }
				]
			}
		},
		methods:{
			changed(){
				this.customize.category = this.category
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
					this.isCategory = false		
				}
			},
			difficulty: function(newVal){
				if(newVal != null){
					this.isDifficulty = false
				}
			}
		}
		
	}
</script>
<style>
	.form{
		margin: auto;
	}
</style>



