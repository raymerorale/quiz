<template>
	<div>
  <!-- <b-nav tabs>
    <b-nav-item disabled><b>Fancy Quiz App</b></b-nav-item>
    <b-nav-item disabled>Counter: <span>{{ index + 1 }}</span>/10</b-nav-item>
    <b-nav-item disabled>Score: <span>{{ numCorrect }}</span></b-nav-item>
  </b-nav> -->
  <b-progress height="2rem" :value="progress*10" class="mb-2"></b-progress>
</div>
</template>
<script>
	export default {
		props:{
			progress: Number
		},
		data(){
			return{
				
			}
		}
	}
</script> 
