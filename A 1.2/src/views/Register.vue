<template>
  <div class="register">
    <!-- register form -->
    <h2>Register</h2>
    <form @submit.prevent="handleRegister">
      <div class="form-group">
        <label>Username:</label>
        <input type="text" v-model="username" required>
      </div>
      
      <div class="form-group">
        <label>Email:</label>
        <input type="email" v-model="email" required>
      </div>
      
      <div class="form-group">
        <label>Password:</label>
        <input type="password" v-model="password" required>
      </div>
      
      <div class="form-group">
        <label>Confirm Password:</label>
        <input type="password" v-model="confirmPassword" required>
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
    // reactive data
    const username = ref('')
    const email = ref('')
    const password = ref('')
    const confirmPassword = ref('')
    
    // register function
    const handleRegister = () => {
      console.log('Register attempt:', username.value)
    }
    
    return {
      username,
      email,
      password,
      confirmPassword,
      handleRegister
    }
  }
}
</script>

<style scoped>
/* register styles with Bootstrap breakpoints */
.register {
  max-width: 400px;
  margin: 0 auto;
  padding: 2rem;
}

.register h2 {
  text-align: center;
  margin-bottom: 2rem;
  color: #333;
}

.form-group {
  margin-bottom: 1.5rem;
}

.form-group label {
  display: block;
  margin-bottom: 0.5rem;
  font-weight: bold;
  color: #333;
}

.form-group input {
  width: 100%;
  padding: 0.75rem;
  border: 1px solid #ddd;
  border-radius: 4px;
  font-size: 1rem;
  transition: border-color 0.3s;
}

.form-group input:focus {
  outline: none;
  border-color: #3498db;
  box-shadow: 0 0 0 2px rgba(52, 152, 219, 0.2);
}

button {
  width: 100%;
  background: #27ae60;
  color: white;
  border: none;
  padding: 0.75rem 1.5rem;
  border-radius: 4px;
  cursor: pointer;
  font-size: 1rem;
  transition: background-color 0.3s;
}

button:hover {
  background: #229954;
}

/* Bootstrap breakpoints implementation */
/* Extra small devices (portrait phones, less than 576px) */
@media (max-width: 575.98px) {
  .register {
    padding: 1rem;
    max-width: 100%;
    margin: 0 0.5rem;
  }
  
  .register h2 {
    font-size: 1.3rem;
    margin-bottom: 1rem;
  }
  
  .form-group {
    margin-bottom: 1rem;
  }
  
  .form-group input {
    padding: 0.6rem;
    font-size: 0.9rem;
  }
  
  button {
    padding: 0.6rem 1rem;
    font-size: 0.9rem;
  }
}

/* Small devices (landscape phones, 576px and up) */
@media (min-width: 576px) and (max-width: 767.98px) {
  .register {
    padding: 1.5rem;
    max-width: 400px;
  }
  
  .register h2 {
    font-size: 1.4rem;
    margin-bottom: 1.5rem;
  }
  
  .form-group {
    margin-bottom: 1.25rem;
  }
  
  .form-group input {
    padding: 0.7rem;
    font-size: 0.95rem;
  }
  
  button {
    padding: 0.7rem 1.25rem;
    font-size: 0.95rem;
  }
}

/* Medium devices (tablets, 768px and up) */
@media (min-width: 768px) and (max-width: 991.98px) {
  .register {
    padding: 2rem;
    max-width: 400px;
  }
  
  .register h2 {
    font-size: 1.5rem;
    margin-bottom: 2rem;
  }
  
  .form-group {
    margin-bottom: 1.5rem;
  }
  
  .form-group input {
    padding: 0.75rem;
    font-size: 1rem;
  }
  
  button {
    padding: 0.75rem 1.5rem;
    font-size: 1rem;
  }
}

/* Large devices (desktops, 992px and up) */
@media (min-width: 992px) and (max-width: 1199.98px) {
  .register {
    padding: 2rem;
    max-width: 400px;
  }
  
  .register h2 {
    font-size: 1.6rem;
    margin-bottom: 2rem;
  }
  
  .form-group {
    margin-bottom: 1.5rem;
  }
  
  .form-group input {
    padding: 0.8rem;
    font-size: 1rem;
  }
  
  button {
    padding: 0.8rem 1.5rem;
    font-size: 1rem;
  }
}

/* Extra large devices (large desktops, 1200px and up) */
@media (min-width: 1200px) {
  .register {
    padding: 2.5rem;
    max-width: 450px;
  }
  
  .register h2 {
    font-size: 1.8rem;
    margin-bottom: 2.5rem;
  }
  
  .form-group {
    margin-bottom: 1.75rem;
  }
  
  .form-group input {
    padding: 0.9rem;
    font-size: 1.1rem;
  }
  
  button {
    padding: 0.9rem 1.75rem;
    font-size: 1.1rem;
  }
}
</style>
