<template>
  <div class="home">
    <h1>Welcome to Youth Mental Health</h1>
    
    <!-- 分类筛选 -->
    <div class="category-filter">
      <button 
        v-for="category in categories" 
        :key="category"
        @click="filterByCategory(category)"
        class="filter-btn"
      >
        {{ category }}
      </button>
    </div>
    
    <!-- 动态资源列表 -->
    <div class="resources-grid">
      <div 
        v-for="resource in filteredResources" 
        :key="resource.id"
        class="resource-card"
      >
        <h3 class="resource-title">{{ resource.title }}</h3>
        <p class="resource-description">{{ resource.description }}</p>
        <span class="resource-category">{{ resource.category }}</span>
      </div>
    </div>
  </div>
</template>

<script>
import { ref, computed, onMounted } from 'vue'
import mentalHealthData from '../data/mentalHealthData.json'

// home page component with dynamic data
export default {
  name: 'Home',
  setup() {
    const resources = ref([])
    const categories = ref([])
    const selectedCategory = ref('All')
    
    const loadData = () => {
      resources.value = mentalHealthData.resources
      categories.value = mentalHealthData.categories
    }
    
    const filterByCategory = (category) => {
      selectedCategory.value = category
    }
    
    const filteredResources = computed(() => {
      if (selectedCategory.value === 'All') {
        return resources.value
      }
      return resources.value.filter(resource => resource.category === selectedCategory.value)
    })
    
    onMounted(() => {
      loadData()
    })
    
    return {
      resources,
      categories,
      selectedCategory,
      filteredResources,
      filterByCategory
    }
  }
}
</script>

<style>
.home {
  max-width: 1000px;
  margin: 0 auto;
  padding: 2rem;
}

.home h1 {
  text-align: center;
  margin-bottom: 2rem;
  color: #333;
}

.category-filter {
  display: flex;
  justify-content: center;
  gap: 1rem;
  margin-bottom: 2rem;
  flex-wrap: wrap;
}

.filter-btn {
  background: #ecf0f1;
  color: #333;
  border: none;
  padding: 0.5rem 1rem;
  border-radius: 20px;
  cursor: pointer;
  transition: all 0.3s;
}

.filter-btn:hover {
  background: #bdc3c7;
}

.resources-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
  gap: 1.5rem;
}

.resource-card {
  background: white;
  padding: 1.5rem;
  border-radius: 10px;
  box-shadow: 0 2px 4px rgba(0,0,0,0.1);
  transition: all 0.3s;
}

.resource-card:hover {
  transform: translateY(-3px);
  box-shadow: 0 4px 8px rgba(0,0,0,0.15);
}

.resource-title {
  color: #333;
  margin-bottom: 0.5rem;
  font-size: 1.1rem;
}

.resource-description {
  color: #666;
  margin-bottom: 1rem;
  line-height: 1.4;
}

.resource-category {
  background: #e3f2fd;
  color: #1976d2;
  padding: 0.25rem 0.5rem;
  border-radius: 4px;
  display: inline-block;
}

/* responsive design */
@media (max-width: 768px) {
  .home {
    padding: 1rem;
  }
  
  .resources-grid {
    grid-template-columns: 1fr;
  }
  
  .category-filter {
    justify-content: center;
  }
  
  .filter-btn {
    margin-bottom: 0.5rem;
  }
}
</style>
