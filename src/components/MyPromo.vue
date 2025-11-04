<template>
    <section class="promo-section" :style="{
        backgroundImage: 'url(' + backgroundImage + ')',
        backgroundPosition: 'top',
        backgroundRepeat: 'no-repeat',
        backgroundSize: 'cover'
    }">
        <div class="container">
            <div class="promo-content">
                <div class="promo-card">
                    <h1 class="promo-title">Найдите нужный проект</h1>
                    <p class="promo-subtitle">Введите название проекта для получения подробной информации</p>
                    
                    <div class="search-container">
                        <div class="search-input-wrapper">
                            <input 
                                v-model="searchQuery"
                                class="search-input" 
                                placeholder="Введите название проекта..."
                                @keypress.enter="handleSearch"
                            >
                            <span class="search-icon">🔍</span>
                        </div>
                        <button class="search-btn" @click="handleSearch">
                            <span>Найти проект</span>
                            <span class="btn-arrow">→</span>
                        </button>
                    </div>

                  
                
                </div>
            </div>
        </div>
    </section>
</template>

<script>
import './ProjectList.vue'
export default {
    name: 'MyPromo',
    data() {
        return {
            searchQuery: '',
            backgroundImage: '' ,
            
            
                }
    },
    methods: {
       async handleSearch() {
            if (this.searchQuery.trim()) {
                 const response= await fetch('/data/projects.json')
                 const data = await response.json()
                     const foundProject = data.projects.find(project => {
                            const projectTitle = project.title.toLowerCase();
                            const searchTerm = this.searchQuery.toLowerCase();
                            return projectTitle.includes(searchTerm);
                        });
                    if(foundProject){
                        console.log('ok')
                        this.$router.push(`/project/${foundProject.id}`);
                    }
                    else console.log('none')
                 }
                 
                
                console.log('Поиск аукциона:', this.searchQuery);
                
            }
        }
    }

</script>

<style scoped>

</style>