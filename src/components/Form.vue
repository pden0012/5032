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
              @blur="() => validateName(true)"
              @input="() => validateName(false)"
            />
            <!-- form-control = bootstrap's magic style. v-model = live sync with formData -->
            <div v-if="errors.username" class="text-danger">{{ errors.username }}</div>
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
              @blur="() => validatePassword(true)"
              @input="() => validatePassword(false)"
            />
            <!-- type=password = hides the text, duh -->
            <div v-if="errors.password" class="text-danger">{{ errors.password }}</div>
          </div>

          <!-- Australian Resident -->
          <div class="mb-3 form-check">
            <!-- form-check = bootstrap style for checkbox -->
            <input
              type="checkbox"
              class="form-check-input"
              id="isAustralian"
              v-model="formData.isAustralian"
              @change="() => validateResident(true)"
            />
            <label class="form-check-label" for="isAustralian">
              Australian Resident?
            </label>
            <div v-if="errors.resident" class="text-danger">{{ errors.resident }}</div>
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
              @blur="() => validateReason(true)"
              @input="() => validateReason(false)"
            ></textarea>
            <!-- textarea = bigger box, rows=3 = not too tall -->
            <div v-if="errors.reason" class="text-danger">{{ errors.reason }}</div>
          </div>

          <!-- Gender -->
          <div class="mb-4">
            <label for="gender" class="form-label">Gender</label>
            <select 
              class="form-select" 
              id="gender" 
              v-model="formData.gender"
              @change="() => validateGender(true)"
            >
              <option disabled value="">Select gender</option>
              <option>Female</option>
              <option>Male</option>
              <option>Other</option>
            </select>
            <!-- form-select = bootstrap dropdown styling -->
            <div v-if="errors.gender" class="text-danger">{{ errors.gender }}</div>
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
            <!-- flex-wrap = so cards don't squeeze, they wrap nicely -->
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

// 这个对象用来存放错误信息，开始都是null（没有错误）
// 当用户输入有问题时，我们就在这里放错误消息
const errors = ref({
  username: null,    // 用户名错误信息
  password: null,    // 密码错误信息
  resident: null,    // 居民身份错误信息
  gender: null,      // 性别错误信息
  reason: null       // 理由错误信息
})

// submittedCards = array of all submissions (cards will be made from this)
const submittedCards = ref([])

// 检查用户名是否合法的函数
// blur = true 表示用户点击了别的地方（失去焦点）
// blur = false 表示用户正在输入
const validateName = (blur) => {
  // 如果用户名少于3个字符就不行
  if (formData.value.username.length < 3) {
    // 只有在失去焦点时才显示错误，避免用户正在输入时就报错
    if (blur) errors.value.username = "Name must be at least 3 characters"
  } else {
    // 用户名合格，清除错误信息
    errors.value.username = null
  }
}

// 检查密码是否够强的函数（这个比较复杂哦）
const validatePassword = (blur) => {
  const password = formData.value.password
  const minLength = 8  // 密码最少要8个字符
  
  // 用正则表达式检查密码里有没有这些东西：
  const hasUppercase = /[A-Z]/.test(password)    // 大写字母 A-Z
  const hasLowercase = /[a-z]/.test(password)    // 小写字母 a-z  
  const hasNumber = /\d/.test(password)          // 数字 0-9
  const hasSpecialChar = /[!@#$%^&*(),.?":{}|<>]/.test(password)  // 特殊符号

  // 一个一个检查，哪里不对就提示哪里
  if (password.length < minLength) {
    if (blur) errors.value.password = `Password must be at least ${minLength} characters`
  } else if (!hasUppercase) {
    if (blur) errors.value.password = "Password must contain at least one uppercase letter"
  } else if (!hasLowercase) {
    if (blur) errors.value.password = "Password must contain at least one lowercase letter"
  } else if (!hasNumber) {
    if (blur) errors.value.password = "Password must contain at least one number"
  } else if (!hasSpecialChar) {
    if (blur) errors.value.password = "Password must contain at least one special character"
  } else {
    // 所有条件都满足，密码合格！
    errors.value.password = null
  }
}

// 检查是否勾选了澳大利亚居民
const validateResident = (blur) => {
  // 如果没有勾选复选框就不行
  if (!formData.value.isAustralian) {
    if (blur) errors.value.resident = "You must confirm Australian residency to proceed"
  } else {
    // 勾选了，没问题
    errors.value.resident = null
  }
}

// 检查是否选择了性别
const validateGender = (blur) => {
  // 如果没选或者是空的就不行
  if (!formData.value.gender || formData.value.gender === '') {
    if (blur) errors.value.gender = "Please select your gender"
  } else {
    // 选了性别，OK！
    errors.value.gender = null
  }
}

// 检查加入理由写得够不够
const validateReason = (blur) => {
  // 理由太短不行（至少10个字符）
  if (formData.value.reason.length < 10) {
    if (blur) errors.value.reason = "Reason must be at least 10 characters"
  } 
  // 理由太长也不行（最多500个字符）
  else if (formData.value.reason.length > 500) {
    if (blur) errors.value.reason = "Reason must not exceed 500 characters"
  } 
  // 长度刚好，通过！
  else {
    errors.value.reason = null
  }
}

// 当用户点击提交按钮时执行这个函数
const submitForm = () => {
  // 先把所有字段都检查一遍（都用true，表示要显示错误）
  validateName(true)
  validatePassword(true)
  validateResident(true)
  validateGender(true)
  validateReason(true)

  // 检查是否有任何错误（如果所有错误都是null就表示没问题）
  if (!errors.value.username && 
      !errors.value.password && 
      !errors.value.resident && 
      !errors.value.gender && 
      !errors.value.reason) {
    // 太好了！没有错误，可以提交表单，把数据加到卡片列表里
    submittedCards.value.push({ ...formData.value })
  }
  // 如果有错误，什么都不做，让用户看到错误信息去修改
}

// 当用户点击清空按钮时执行这个函数
const clearForm = () => {
  // 把表单数据全部重置为空
  formData.value = {
    username: '',           // 用户名清空
    password: '',           // 密码清空
    isAustralian: false,    // 复选框取消勾选
    reason: '',             // 理由清空
    gender: ''              // 性别重置为未选择
  }
  
  // 把所有错误消息也清掉
  errors.value = {
    username: null,
    password: null,
    resident: null,
    gender: null,
    reason: null
  }
  
  // 如果你想把下面的卡片也一起清掉，取消下面这行的注释
  // submittedCards.value = []
}
</script>