<template>
  <div id="app">
    <!-- main navigation bar here -->
    <nav class="navbar">
      <div class="nav-brand">Youth Mental Health</div>
      <button class="mobile-menu-toggle" @click="toggleMobileMenu" :class="{ active: mobileMenuOpen }">
        <span></span>
        <span></span>
        <span></span>
      </button>
      <div class="nav-links" :class="{ active: mobileMenuOpen }">
        <router-link to="/" @click="closeMobileMenu">Home</router-link>
        <router-link to="/login" @click="closeMobileMenu">Login</router-link>
        <!-- this is for the register page -->
        <router-link to="/register" @click="closeMobileMenu">Register</router-link>
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
import { ref } from 'vue'

// this is the main app component
export default {
  name: 'App',
  // setup function for composition API
  setup() {
    // mobile menu state
    const mobileMenuOpen = ref(false)
    
    // function to toggle mobile menu
    const toggleMobileMenu = () => {
      mobileMenuOpen.value = !mobileMenuOpen.value
    }
    
    // function to close mobile menu
    const closeMobileMenu = () => {
      mobileMenuOpen.value = false
    }
    
    return {
      mobileMenuOpen,
      toggleMobileMenu,
      closeMobileMenu
    }
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
  display: flex;
  justify-content: space-between;
  align-items: center;
  position: relative;
}

.nav-brand {
  font-size: 1.5rem;
  font-weight: bold;
}

.mobile-menu-toggle {
  display: none;
  flex-direction: column;
  background: none;
  border: none;
  cursor: pointer;
  padding: 0.5rem;
}

.mobile-menu-toggle span {
  width: 25px;
  height: 3px;
  background: white;
  margin: 3px 0;
  transition: 0.3s;
}

.mobile-menu-toggle.active span:nth-child(1) {
  transform: rotate(-45deg) translate(-5px, 6px);
}

.mobile-menu-toggle.active span:nth-child(2) {
  opacity: 0;
}

.mobile-menu-toggle.active span:nth-child(3) {
  transform: rotate(45deg) translate(-5px, -6px);
}

.nav-links {
  display: flex;
  gap: 1rem;
}

.nav-links a {
  color: white;
  text-decoration: none;
  padding: 0.5rem 1rem;
  border-radius: 4px;
  transition: background-color 0.3s;
}

.nav-links a:hover {
  background-color: rgba(255, 255, 255, 0.1);
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

/* Responsive design - Tablet devices */
@media (max-width: 768px) {
  .main-content {
    padding: 1rem;
  }
  
  .nav-brand {
    font-size: 1.2rem;
  }
}

/* Responsive design - Mobile devices */
@media (max-width: 480px) {
  .mobile-menu-toggle {
    display: flex;
  }
  
  .nav-links {
    position: absolute;
    top: 100%;
    left: 0;
    right: 0;
    background: #667eea;
    flex-direction: column;
    padding: 1rem;
    transform: translateY(-100%);
    opacity: 0;
    visibility: hidden;
    transition: all 0.3s ease;
  }
  
  .nav-links.active {
    transform: translateY(0);
    opacity: 1;
    visibility: visible;
  }
  
  .nav-links a {
    padding: 1rem;
    text-align: center;
    border-bottom: 1px solid rgba(255, 255, 255, 0.1);
  }
  
  .nav-links a:last-child {
    border-bottom: none;
  }
  
  .main-content {
    padding: 0.5rem;
  }
  
  .nav-brand {
    font-size: 1rem;
  }
}
</style>
