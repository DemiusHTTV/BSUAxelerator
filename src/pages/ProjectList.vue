

<template>
<section class="bg-body-tertiary">
    <div class="py-5 container">
        <div class="py-5">
            <h2 class="text-center mx-auto">Список проектов</h2>
            <div class="row row-cols-1 row-cols-md-3 g-4">                    
                <div v-for="(item,index) in projectItems" :key="index">
                    <ProjectItem :projectData="item"/>
                </div>
            </div>
           
            &nbsp;&nbsp;&nbsp;<button v-if="showButton" class="btn btn-info btn-md mt-5" @click="LoadByButton">Загрузить проекты</button>
        </div>
    </div>
</section>
</template>

<script>
import ProjectItem from './ProjectItem.vue';
import axios from 'axios';

export default {
name: 'ProjectList',
components: { ProjectItem },
data() {
    return {
        projectItems: [],
        showButton: true
    };
},
methods: {
    LoadByButton() {
        this.showButton = false;
        this.LoadProjects(10);
    },
    LoadProjects(n) {
        console.log("Load projects run!");
        let env = this;
        env.projectItems = [];
        for (let projectId = 1; projectId <= 10; projectId++){
        axios.get('https://webcomp.bsu.ru/api/2025/project_bids/'+projectId)
            .then(function (response) {
                let data = response.data.data;
                for (let i = 0; i < data.length; i++) {
                    env.projectItems.push(data[i]);
                    if (i >= n - 1) {
                        break;
                    }
                }
            })
            .catch(function (error) {
                console.log(error);
            });
        }
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