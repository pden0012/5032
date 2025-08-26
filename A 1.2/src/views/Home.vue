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

.hero button {
  background: #e74c3c;
  color: white;
  border: none;
  padding: 1rem 2rem;
  border-radius: 5px;
  cursor: pointer;
}

.features {
  padding: 2rem 0;
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
}
</style>
