<template>
  <div class="register">
    <h2>Register</h2>
    <!-- registration form -->
    <form @submit.prevent="handleRegister">
      <div class="form-group">
        <label>Email:</label>
        <input type="email" v-model="email" required>
      </div>
      
      <div class="form-group">
        <label>Password:</label>
        <input type="password" v-model="password" required>
      </div>
      
      <button type="submit">Register</button>
    </form>
  </div>
</template>

<script>
import { ref } from 'vue'
// register component
export default {
  name: 'Register',
  setup() {
    // form data
    const email = ref('')
    const password = ref('')
    
    // register function
    const handleRegister = () => {
      console.log('Register attempt:', email.value)
    }
    
    return {
      email,
      password,
      handleRegister
    }
  }
}
</script>

<style scoped>
/* register styles */
.register {
  max-width: 400px;
  margin: 0 auto;
  padding: 2rem;
}

.form-group {
  margin-bottom: 1rem;
}

.form-group label {
  display: block;
  margin-bottom: 0.5rem;
}

.form-group input {
  width: 100%;
  padding: 0.5rem;
  border: 1px solid #ddd;
  border-radius: 4px;
}

button {
  background: #27ae60;
  color: white;
  border: none;
  padding: 0.75rem 1.5rem;
  border-radius: 4px;
  cursor: pointer;
}
</style>
