<template>
    <div class="col">
        <div class="card h-100">
            <div class="project-img">
                <img :src=getImgPath(imgSrc) class="card-img-top" alt="Project">
                <div :class="['card-rating',getRating(rating)]">
                    <span class="fs-2 text-white">{{ rating }}</span>
                </div>
            </div>
            <div class="card-body">
                <h5 class="card-title">{{ title }}</h5>
                <p class="card-text">{{ content }}</p>
            </div>
            <div class="my-3 px-3">
                <span class="badge bg-info" v-for="(item,index) in getTags(tags)" :key="index">{{ item }}</span>&nbsp;&nbsp;                
            </div>
            <div class="my-3 px-3">
                <router-link :to="{name:'projectPage',params:{id:projectId}}" class="text-decoration-none text-success">Подробнее</router-link>                
            </div>
        </div>
    </div>
</template>
<script>
export default{
    name:'ProjectItem',    
    props:['projectData'],
    methods:{
        getRating(rating){
            if(rating<=0){
                return "rating-bg-bad"
            }
            else if(rating<=1.5){
                return "rating-bg-good"
            }
            else if(rating<=3){
                return "rating-bg-perfect"
            }
            else{
                return 
            }
        },
        getImgPath(img){
            return "./img/"+img;
        },
        getTags(tags){
            if (tags && typeof tags === 'string') {
                return tags.split(',')
            } else {
                console.warn("Tags is undefined or not a string. Returning empty array.");
                return [];
            }
        }
        
    },
    data(){
        return{
            projectId: this.projectData.project.id, 
        imgSrc: this.projectData.project.image,   
        rating: this.projectData.project.mark,    
        title: this.projectData.project.title,    
        content: this.projectData.project.description,
        relevance: this.projectData.project.relevance, 
        tags: this.projectData.project.tags
        }
    }
}
</script>
