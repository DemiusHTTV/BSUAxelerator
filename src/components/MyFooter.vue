<template>
    <div class="footer">
<h3 class="mt">{{ currenYear + message }}</h3>
			</div>
</template>
<script>
export default{
    name:'MyFooter',
	components:{

	},
	data(){
		return{
			currenYear: new Date().getFullYear(),
			message:' © IT-Bur'
		}
	}
    }

</script>