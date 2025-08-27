<template>
  <div class="home">
    <!-- hero section with title -->
    <div class="hero">
      <h1>Welcome to Youth Mental Health</h1>
      <p>Support for young people aged 12-25</p>
      <!-- buttons for actions -->
      <button @click="showHelp">Get Help Now</button>
    </div>
    
    <!-- features section -->
    <div class="features">
      <h2>Our Services</h2>
      <div class="feature-grid">
        <div class="feature">
          <h3>Program Finder</h3>
          <p>Find mental health programs</p>
        </div>
        <div class="feature">
          <h3>Resources</h3>
          <p>Articles and videos</p>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
// home page component
export default {
  name: 'Home',
  // composition API setup
  setup() {
    // function to show help
    const showHelp = () => {
      alert('Emergency: 13 11 14')
    }
    
    return {
      showHelp
    }
  }
}
</script>

<style scoped>
/* home page styles */
.home {
  max-width: 800px;
  margin: 0 auto;
  padding: 2rem;
}

.hero {
  text-align: center;
  padding: 3rem 1rem;
  background: #f0f0f0;
  border-radius: 10px;
  margin-bottom: 2rem;
}

.hero h1 {
  font-size: 2rem;
  color: #333;
  margin-bottom: 1rem;
}

.hero p {
  font-size: 1.1rem;
  color: #666;
  margin-bottom: 2rem;
}

.hero button {
  background: #e74c3c;
  color: white;
  border: none;
  padding: 1rem 2rem;
  border-radius: 5px;
  cursor: pointer;
  font-size: 1rem;
  transition: background-color 0.3s;
}

.hero button:hover {
  background: #c0392b;
}

.features {
  padding: 2rem 0;
}

.features h2 {
  text-align: center;
  margin-bottom: 2rem;
  color: #333;
}

.feature-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
  gap: 1rem;
}

.feature {
  background: white;
  padding: 1.5rem;
  border-radius: 8px;
  box-shadow: 0 2px 4px rgba(0,0,0,0.1);
  text-align: center;
  transition: transform 0.3s, box-shadow 0.3s;
}

.feature:hover {
  transform: translateY(-2px);
  box-shadow: 0 4px 8px rgba(0,0,0,0.15);
}

.feature h3 {
  color: #333;
  margin-bottom: 1rem;
}

.feature p {
  color: #666;
}

/* Responsive design - Tablet devices */
@media (max-width: 768px) {
  .home {
    padding: 1rem;
  }
  
  .hero {
    padding: 2rem 1rem;
  }
  
  .hero h1 {
    font-size: 1.5rem;
  }
  
  .hero p {
    font-size: 1rem;
  }
  
  .feature-grid {
    grid-template-columns: 1fr;
    gap: 1rem;
  }
}

/* Responsive design - Mobile devices */
@media (max-width: 480px) {
  .home {
    padding: 0.5rem;
  }
  
  .hero {
    padding: 1.5rem 0.5rem;
    margin-bottom: 1rem;
  }
  
  .hero h1 {
    font-size: 1.3rem;
  }
  
  .hero p {
    font-size: 0.9rem;
    margin-bottom: 1.5rem;
  }
  
  .hero button {
    padding: 0.8rem 1.5rem;
    font-size: 0.9rem;
  }
  
  .features {
    padding: 1rem 0;
  }
  
  .features h2 {
    font-size: 1.3rem;
    margin-bottom: 1rem;
  }
  
  .feature {
    padding: 1rem;
  }
  
  .feature h3 {
    font-size: 1.1rem;
  }
  
  .feature p {
    font-size: 0.9rem;
  }
}
</style>
