<template>
	<MyPromo v-if="showPromo"></MyPromo>
	<section class="">


	<!--<a href="about.html#/about" class="btn btn-success btn-md text-white mt-5">Больше информации</a>-->
			
		
	</section>
	<ProjectList />
</template>
<script>
import MyPromo from './MyPromo.vue';
import ProjectList from './ProjectList.vue';

export default {
	name: 'MyMain',
	props: {
		showPromo: Boolean
	},
	components: { MyPromo, ProjectList }
}
</script>