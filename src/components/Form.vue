<template>
  <div class="container mt-5">
    <!-- ok so bootstrap "container" here... kinda like a centered box with some margin top -->
    <div class="row justify-content-center">
      <!-- row = horizontal line thing. justify-content-center means: push stuff to the middle -->

      <div class="col-12 col-sm-10 col-md-8 col-lg-6 col-xl-5">
        <!-- 
          breakpoints magic:
          - col-12 = on tiny phone, take the whole line
          - col-sm-10 = on small devices, leave a lil margin
          - col-md-8 = on medium (ipad-ish), shrink more
          - col-lg-6 = on laptop, half-half style
          - col-xl-5 = on big screens, even skinnier
          so yeah, this box keeps resizing, looks nice everywhere 😅
        -->

        <h1 class="text-center mb-4">User Information Form / Credentials</h1>
        <!-- center the title cuz it just looks wayyy better in the middle -->

        <form @submit.prevent="submitForm">
          <!-- so yeah, the form. prevent = stop the browser from reloading -->

          <!-- Username -->
          <div class="mb-3">
            <!-- mb-3 = lil bottom margin -->
            <label for="username" class="form-label">Username</label>
            <input
              type="text"
              class="form-control"
              id="username"
              v-model="formData.username"
              placeholder="Enter your username"
            />
            <!-- form-control = bootstrap's magic style. v-model = live sync with formData -->
          </div>

          <!-- Password -->
          <div class="mb-3">
            <label for="password" class="form-label">Password</label>
            <input
              type="password"
              class="form-control"
              id="password"
              v-model="formData.password"
              placeholder="Enter a password"
            />
            <!-- type=password = hides the text, duh -->
          </div>

          <!-- Australian Resident -->
          <div class="mb-3 form-check">
            <!-- form-check = bootstrap style for checkbox -->
            <input
              type="checkbox"
              class="form-check-input"
              id="isAustralian"
              v-model="formData.isAustralian"
            />
            <label class="form-check-label" for="isAustralian">
              Australian Resident?
            </label>
          </div>

          <!-- Reason -->
          <div class="mb-3">
            <label for="reason" class="form-label">Reason For Joining</label>
            <textarea
              class="form-control"
              id="reason"
              rows="3"
              v-model="formData.reason"
              placeholder="Tell us why you join"
            ></textarea>
            <!-- textarea = bigger box, rows=3 = not too tall -->
          </div>

          <!-- Gender -->
          <div class="mb-4">
            <label for="gender" class="form-label">Gender</label>
            <select class="form-select" id="gender" v-model="formData.gender">
              <option disabled value="">Select gender</option>
              <option>Female</option>
              <option>Male</option>
              <option>Other</option>
            </select>
            <!-- form-select = bootstrap dropdown styling -->
          </div>

          <!-- buttons row -->
          <div class="d-grid gap-2 d-sm-flex">
            <!-- d-grid = stack on tiny screens. d-sm-flex = side-by-side on bigger ones -->
            <button type="submit" class="btn btn-primary me-sm-2">Submit</button>
            <!-- btn-primary = blue button -->
            <button type="button" class="btn btn-secondary" @click="clearForm">Clear</button>
            <!-- btn-secondary = grey button -->
          </div>
        </form>

        <!-- submitted cards go here -->
        <div class="row mt-5" v-if="submittedCards.length">
          <!-- only show this if there's something inside submittedCards -->
          <div class="d-flex flex-wrap justify-content-start">
            <!-- flex-wrap = so cards don’t squeeze, they wrap nicely -->
            <div v-for="(card, index) in submittedCards" :key="index" class="card m-2" style="width: 18rem;">
              <!-- loop all submitted data and make a lil card for each one -->
              <div class="card-header">User Information</div>
              <ul class="list-group list-group-flush">
                <li class="list-group-item">Username: {{ card.username }}</li>
                <li class="list-group-item">Password: {{ card.password }}</li>
                <li class="list-group-item">Australian Resident: {{ card.isAustralian ? 'Yes' : 'No' }}</li>
                <li class="list-group-item">Gender: {{ card.gender }}</li>
                <li class="list-group-item">Reason: {{ card.reason }}</li>
              </ul>
            </div>
          </div>
        </div>

      </div>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue'

// so yeah, we need some reactive stuff (reactive = Vue auto tracks changes)

// the form data, live updated with v-model
const formData = ref({
  username: '',      // start empty
  password: '',      // also empty
  isAustralian: false, // checkbox default unchecked
  reason: '',        // textarea
  gender: ''         // select dropdown
})

// submittedCards = array of all submissions (cards will be made from this)
const submittedCards = ref([])

const submitForm = () => {
  // basically just copy whatever’s inside formData and push it into submittedCards
  submittedCards.value.push({ ...formData.value })
}

const clearForm = () => {
  // reset form back to empty
  formData.value = {
    username: '',
    password: '',
    isAustralian: false,
    reason: '',
    gender: ''
  }
  // if u also wanna wipe all cards, just uncomment below
  // submittedCards.value = []
}
</script>