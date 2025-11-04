<template>
  <div class="card h-100">
    <div class="project-img">
      <img :src="getImgPath(imgSrc)" class="card-img-top" alt="Project">
      <div :class="['card-rating', getRating(rating)]">
        <span class="fs-2 text-white">{{ rating }}</span>
      </div>
    </div>
    <div class="card-body">
      <h5 class="card-title">{{ title }}</h5>
      <p class="card-text">{{ content }}</p>
    </div>
    <div class="my-3 px-3">
      <span class="badge bg-info" v-for="(item,index) in getTags(tags)" :key="index">{{ item }}</span>                
    </div>
    <div class="my-3 px-3">
      <router-link :to="{name:'projectPage',params:{id:projectId}}" class="text-decoration-none text-success">Подробнее</router-link>                
    </div>
  </div>
</template>

<script>
export default {
  name: 'ProjectItem',    
  props: {
    projectData: {
      type: Object,
      required: true
    }
  },
  computed: {
    projectId() { return this.projectData.id },
    imgSrc() { return this.projectData.image },
    rating() { return this.projectData.mark }, // На всякий случай
    title() { return this.projectData.title },
    content() { return this.projectData.description },
    tags() { return this.projectData.tags }
  },
  methods: {
    getRating(rating) {
      if (rating >= 4.5) return "rating-bg-perfect"
      else if (rating >= 4.0) return "rating-bg-good"
      else return "rating-bg-bad"
    },
    getImgPath(img) {
      return "./img/" + img;
    },
    getTags(tags) {
      return tags ? tags.split(',') : [];
    }
  }
}
</script>