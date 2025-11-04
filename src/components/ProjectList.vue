<template>
  <section class="bg-body-tertiary">
    <div class="py-5 container">
      <div class="py-5">
        
        <h2 class="text-center mx-auto">Список проектов</h2>
        
        <!-- Показываем загрузку -->
        <div v-if="loading" class="text-center">
          <div class="spinner-border text-primary" role="status">
            <span class="visually-hidden">Загрузка...</span>
          </div>
          <p class="mt-2">Загружаем проекты...</p>
        </div>
        
        <!-- Показываем проекты -->
        <div v-else class="row row-cols-1 row-cols-md-3 g-4">
          <div v-for="project in projects" :key="project.id" class="col">
            <ProjectItem :projectData="project" />
          </div>
        </div>
        
        <!-- Кнопка для загрузки еще -->
        <div v-if="!loading && showLoadMore" class="text-center mt-4">
          <button class="btn btn-info btn-lg" @click="loadMoreProjects">
            Загрузить еще проекты
          </button>
        </div>
      </div>
    </div>
  </section>
</template>

<script>
import ProjectItem from "./ProjectItem.vue";

export default {
  name: "ProjectList",
  components: { ProjectItem },
  data() {
    return {
      projects: [],
      loading: false,
      showLoadMore: true,
      currentPage: 1,
      projectsPerPage: 3
    };
  },
  methods: {
    // Убрал async из methods - просто объявляем функцию
    loadProjects() {
      this.loading = true;
      
      fetch('/data/projects.json')
        .then(response => response.json())
        .then(data => {
          // Загружаем только часть проектов для пагинации
          const startIndex = (this.currentPage - 1) * this.projectsPerPage;
          const endIndex = startIndex + this.projectsPerPage;
          const projectsToShow = data.projects.slice(startIndex, endIndex);
          
          this.projects = [...this.projects, ...projectsToShow];
          this.loading = false;
          
          // Проверяем, есть ли еще проекты для загрузки
          this.showLoadMore = endIndex < data.projects.length;
        })
        .catch(error => {
          console.error('Ошибка загрузки:', error);
          this.loading = false;
          this.loadFallbackProjects();
        });
    },
    
    loadMoreProjects() {
      this.currentPage++;
      this.loadProjects();
    },
    
    loadFallbackProjects() {
      this.projects = [
        {
          id: 1,
          title: "EcoClean - мобильное приложение для уборки мусора",
          description: "Инновационное мобильное приложение для экологической уборки",
          image: "project_1.jpg",
          tags: "EcoNet, мобильное приложение",
          mark: 4.8
        },
        {
          id: 2,
          title: "PsyKids - платформа для школьных психологов",
          description: "Комплексное решение для автоматизации работы психологов", 
          image: "project_2.jpg",
          tags: "HealthNet, EduNet",
          mark: 4.9
        },
        {
          id: 3,
          title: "BePed.ru - образовательный портал для педагогов",
          description: "Современная онлайн-платформа для педагогов",
          image: "project_3.jpg",
          tags: "EduNet, веб-сайт",
          mark: 4.7
        }
      ];
      this.showLoadMore = false;
    }
  },
  mounted() {
    // Загружаем первые проекты при монтировании
    this.loadProjects();
  }
};
</script>