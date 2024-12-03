<template>
  <div class="bubble-background">
    <!-- Moving Bubbles -->
    <div class="bubbles">
      <div
        v-for="n in 100"
        :key="n"
        class="bubble"
        :style="generateBubbleStyle()"
        @mouseover="removeBubble"
      ></div>
    </div>

    <!-- Login Form -->
    <div class="login-container">
      <div :class="['card p-4 custom-card', currentTheme]">
        <h2 class="login-heading">Login</h2>
        <form @submit.prevent="handleLogin">
          <div class="form-group mb-3">
            <label for="email" class="form-label">Username or Email</label>
            <div class="input-group">
              <span class="input-group-text">
                <i class="fas fa-envelope"></i>
              </span>
              <input 
                type="email" 
                class="form-control custom-input" 
                id="email" 
                v-model="email" 
                placeholder="Enter your Username or Email" 
                required 
              />
            </div>
          </div>
          <div class="form-group mb-3">
            <label for="password" class="form-label">Password</label>
            <div class="input-group">
              <span class="input-group-text">
                <i class="fas fa-lock"></i>
              </span>
              <input 
                :type="showPassword ? 'text' : 'password'" 
                class="form-control custom-input" 
                id="password" 
                v-model="password" 
                placeholder="Enter your password" 
                required 
              />
              <button 
                type="button" 
                class="btn password-toggle" 
                :class="currentTheme"
                @click="togglePasswordVisibility"
                :aria-label="showPassword ? 'Hide password' : 'Show password'"
              >
                <i :class="showPassword ? 'fas fa-eye-slash' : 'fas fa-eye'"></i>
              </button>
            </div>
          </div>
          <button type="submit" class="btn custom-btn w-100" :class="currentTheme">
            <i class="fas fa-sign-in-alt"></i> Login
          </button>
          <p v-if="errorMessage" class="text-danger text-center mt-2">{{ errorMessage }}</p>
        </form>
      </div>
    </div>
  </div>
</template>

<script>
import { useRouter } from 'vue-router';
const router = useRouter()
export default {
  data() {
    return {
      email: '',
      password: '',
      showPassword: false,
      errorMessage: '',
    };
  },
  computed: {
    currentTheme() {
      return this.$root.currentTheme; // Dynamically access theme (light/dark)
    },
  },
  methods: {
    handleLogin() {
      const validEmail = 'jun@gmail.com';
      const validPassword = 'admin';
      if (this.email === validEmail && this.password === validPassword) {
        alert('Login successful!');
      router.push('/portfolio/profile')
      } else {
        this.errorMessage = 'Invalid email or password. Please try again.';
      }
    },
    togglePasswordVisibility() {
      this.showPassword = !this.showPassword;
    },
    // Generate style for bubbles without response to typing
    generateBubbleStyle() {
      const size = `${Math.random() * 50 + 10}px`;
      const shape = Math.random() > 0.5 ? '50%' : `${Math.random() * 50 + 50}% ${Math.random() * 50 + 50}%`;
      const animationDuration = `${Math.random() * 10 + 5}s`; // Random float-up duration
      const animationDelay = `${Math.random() * 5}s`; // Random delay to stagger animation

      return {
        width: size,
        height: size,
        borderRadius: shape,
        animationDuration,
        animationDelay,
        left: `${Math.random() * 100}%`, // Random horizontal position
      };
    },
    // Remove bubble when hovered
    removeBubble(event) {
      // Make the bubble disappear when hovered
      event.target.style.opacity = '0';
      setTimeout(() => {
        event.target.style.display = 'none'; // Hide the bubble after it disappears
      }, 300); // Allow for fade effect before removing the element
    },
  },
};
</script>

<style scoped>
:root {
  --primary-bg-color: #007bff;
  --accent-color: #0056b3;
  --primary-text-color: #333;
  --light-border: #ddd;
  --dark-border: #fcfdfb;
}

/* Dynamic background for bubbles */
.bubble-background {
  position: relative;
  width: 100vw;
  height: 100vh;
  overflow: hidden;
  background: var(--primary-bg-color);
  transition: background-color 0.3s ease;
}

/* Moving Bubbles */
.bubbles {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  z-index: 0;
  pointer-events: none;
}

.bubble {
  position: absolute;
  bottom: -50px;
  background: rgba(0, 123, 255, 0.4);
  animation: floatUp linear infinite;
}

.bubble:nth-child(odd) {
  background: rgba(30, 144, 255, 0.6);
}

.bubble:nth-child(even) {
  background: rgba(0, 86, 179, 0.8);
}

@keyframes floatUp {
  0% {
    transform: translateY(0);
    opacity: 0.8;
  }
  50% {
    transform: translateY(-50vh);
    opacity: 1;
  }
  100% {
    transform: translateY(-100vh);
    opacity: 0;
  }
}

/* Login Form */
.login-container {
  position: absolute;
  bottom: 20px;
  left: 20px;
  width: 100%;
  display: flex;
  justify-content: flex-start;
  align-items: flex-end;
  z-index: 1;
}

.custom-card {
  background-color: rgba(255, 255, 255, 0.9);
  color: var(--primary-text-color);
  border-radius: 15px;
  box-shadow: 0px 4px 15px rgba(0, 0, 0, 0.1);
  max-width: 400px;
  width: 100%;
  transition: background 0.5s ease;
}

/* Light/Dark Modes for Login Button and Toggle Button */
.light-theme .custom-btn,
.light-theme .password-toggle {
  background-color: #007bff;
  color: #070707;
}

.dark-theme .custom-btn,
.dark-theme .password-toggle {
  background-color: #0056b3;
  color: #fdfdfd;
}

.custom-btn:hover,
.password-toggle:hover {
  opacity: 0.9;
}

.password-toggle {
  border: none;
  cursor: pointer;
  transition: background-color 0.3s ease;
}

/* Theming for light and dark modes */
.light-theme .custom-card {
  background-color: #ffffff;
  color: var(--primary-text-color);
}

.dark-theme .custom-card {
  background-color: rgba(0, 0, 0, 0.8);
  color: #fff;
}
</style>
