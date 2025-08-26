<template>
  <div id="app">
    <!-- main navigation bar here -->
    <nav class="navbar">
      <div class="nav-brand">Youth Mental Health</div>
      <div class="nav-links">
        <router-link to="/">Home</router-link>
        <router-link to="/login">Login</router-link>
        <!-- this is for the register page -->
        <router-link to="/register">Register</router-link>
      </div>
    </nav>
    
    <!-- main content area -->
    <main class="main-content">
      <router-view />
    </main>
    
    <!-- footer section at bottom -->
    <footer class="footer">
      <p>&copy; 2025 Youth Mental Health Support</p>
    </footer>
  </div>
</template>

<script>
// this is the main app component
export default {
  name: 'App',
  // setup function for composition API
  setup() {
    // just return empty object for now
    return {}
  }
}
</script>

<style>
/* basic styling */
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

body {
  font-family: Arial, sans-serif;
}

#app {
  min-height: 100vh;
  display: flex;
  flex-direction: column;
}

.navbar {
  background: #667eea;
  padding: 1rem;
  color: white;
}

.nav-brand {
  font-size: 1.5rem;
  font-weight: bold;
}

.nav-links {
  display: flex;
  gap: 1rem;
}

.nav-links a {
  color: white;
  text-decoration: none;
}

.main-content {
  flex: 1;
  padding: 2rem;
}

.footer {
  background: #333;
  color: white;
  text-align: center;
  padding: 1rem;
}
</style>
