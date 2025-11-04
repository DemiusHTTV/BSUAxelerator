<template>
    <div class="container d-flex flex-column gap-5" v-if="item">
      <h1>{{ item.title }}</h1>
      <div class="row">
        <div class="col-3">
          <img :src="item.image" class="card-img-top" />
        </div>
        <div class="col-8">
          <p>{{ item.description }}</p>
            </div>
      </div>
    </div>
    <div v-else>
      Загрузка...
    </div>
  </template>
  
  <script>
  
  
  export default {
    name: 'ProjectPage',
    data() {
      return {
        id: null, 
        item: null, 
      };
    },
    created() {
      const record_id = parseInt(this.$route.params.id, 10);
  
      if (record_id) {
        this.id = record_id;
        this.getProject(record_id); // Вызываем асинхронный метод
      } else {
        console.warn("No project ID provided in route parameters.");
      }
    },
    methods: {
      async getProject(record_id) {
        try {
          const response = await fetch('/data/projects.json')
          const data = await response.json() 
const foundProject = data.projects.find(project => 
  project.id === record_id 
);
if(foundProject){
  this.item =foundProject
}

  
                else {
               this.item = null; 
            console.warn(`Project with id ${record_id} not found in API.`);
          }
        } catch (error) {
            this.item = null;
          console.error("Error fetching project:", error);
        }
      },
    },
  };
  </script>
  