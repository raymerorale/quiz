<template>
	<b-card class="border-0 rounded-0 shadow w-100">
		<div class="col-12 col-md-6 col-lg-5 m-auto">
			<b-nav pills>
				<b-nav-item class='h4'>
					<span class='orange'>{{ category }}</span>
				</b-nav-item>
				<b-nav-item disabled 
					class="text-capitalize mr-sm-auto mt-1">{{ difficulty }}
				</b-nav-item>
				<b-nav-item class="ml-auto h4 bg-orange rounded">
					<span class='text-light'>{{ score }}</span>
				</b-nav-item>
			</b-nav>
			<b-progress variant='warning' animated height="1rem" :value="progress*10" class="rounded-pill"></b-progress>
		</div>
	</b-card>
</template>
<script>
	export default {
		props:{
			score: Number,
			progress: Number,
			category: String,
			difficulty: String
		},
		data(){
			return{
				
			}
		}
	}
</script> 
<style>
	.orange{
		color: #FA9F42 !important;
	}
	.bg-orange{
		background: #FA9F42 !important;
	}
</style>
