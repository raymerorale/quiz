<template>
	<div>
  <b-nav tabs>
    <b-nav-item disabled><b>Fancy Quiz App</b></b-nav-item>
    <b-nav-item disabled>Counter: <span>{{ index + 1 }}</span>/10</b-nav-item>
    <b-nav-item disabled>Score: <span>{{ numCorrect }}</span></b-nav-item>
  </b-nav>
</div>
</template>
<script>
	export default {
		props:{
			index: Number,
			numCorrect: Number
		}
	}
</script> 
