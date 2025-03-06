<template>
    <section class="bg-body-tertiary">
        <div class="py-5 container">
            <div class="py-5">
                <h2 class="text-center mx-auto">Список проектов</h2>
                <div class="row row-cols-1 row-cols-md-3 g-4">                    
                    <ProjectItem v-for="(item,index) in projectItems" :key="index" :projectData="item"/>
                    
                </div>
                <a href="/ProjectList" class="btn btn-success btn-md mt-5">Смотреть весь список</a> 
                &nbsp;&nbsp;&nbsp;<button v-if="showButton" class="btn btn-info btn-md mt-5" @click="LoadByButton">Загрузить проекты</button>
            </div>
        </div>
    </section>
</template>
<script>
import ProjectItem from './ProjectItem.vue';
import axios from 'axios';
export default{
    name: 'ProjectList',
    components: {  ProjectItem },
    data(){
        return {
            projectItems:[
               
            ],
            showButton:true,
             
        }
    },
    methods:{
        LoadByButton(){
            this.showButton=false
            

            this.LoadProjects(10)
        },
        LoadProjects(n){//параметр n
            console.log("Load projects run!");            
            let env=this;
            env.projectItems=[]
           let b=3;
            axios.get('https://webcomp.bsu.ru/api/2025/project_bids/'+b)
            
        
            .then(function (response) {
                // обработка успешного запроса
            console.log('https://webcomp.bsu.ru/api/2025/project_bids/'+b)    
                let data=response["data"]["data"];
                //console.log(data);
                b++;
                for (let i=0;i<data.length;i++){
                   
                    env.projectItems.push(data[i])
                 
                
                    if(i>=n-1){
                        break
                    }
                }                
            })
        
            .catch(function (error) {
                // обработка ошибки
                console.log(error);
            })
            .finally(function () {
                // выполняется всегда
            });
        }
        
    },
    mounted() {
        axios.get('api/projects')
            .then(response => {
                this.projects = response.data;
            })
            .catch(error => {
                console.error(error);
            });
    }
};
</script>

