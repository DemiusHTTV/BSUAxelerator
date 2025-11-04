<template>
	
		<div class ='backLogo'>
		<p v-if="error" class="error-message">{{ error }}</p>
		<LoginForm v-model:login="login" v-model:password="password" @sendData="sendData()"/>
		<p class="mt-5 mb-3 text-muted">{{ currentYear }}  {{ message }}</p>
	</div>
  </template>

<script>
import LoginForm from '../components/forms/LoginForm.vue'

export default {
    name: 'LoginPage',
	beforeCreate(){
		document.body.className='text-center',
		document.getElementById("app").style.width="100%"		
	},
    components: {        
		LoginForm
    },
	data(){
    return{
      login:'',
      password:'',
      error: '',
      currentYear: new Date().getFullYear(),
      message: ' © IT-Bur'
    }
},
	methods:{
		sendData(){
			this.$store.dispatch('login',{'login':this.login,'password':this.password})
			.then(()=>this.$router.push({path:'/admin'}))
			.catch(()=>{
				this.error="Неправильный логин или пароль";
				console.log("Неправильный логин или пароль")
				alert("Неправильный логин или пароль")
			})
		}
	}

}
</script>
<style scoped src="@/assets/css/signin.css"></style>

