<template>
  <div id="app" :class="currentTheme">
    <NavBar v-if="!shouldHideNavBar" />
    <router-view />
    <ThemeToggle :currentTheme="currentTheme" @themeToggle="ThemeToggle" />
  </div>
</template>

<script>
import NavBar from './components/NavBar.vue';
import ThemeToggle from './components/ThemeToggle.vue'; // Import the new ThemeToggle component

export default {
  components: {
    NavBar,
    ThemeToggle,
  },
  data() {
    return {
      currentTheme: 'light-theme', // Default theme
    };
  },
  computed: {
    shouldHideNavBar() {
      return this.$route.meta.hideNavBar === true && this.$route.name !== 'Login';
    },
  },
  methods: {
    ThemeToggle() {
      this.currentTheme = this.currentTheme === 'light-theme' ? 'dark-theme' : 'light-theme';
    },
  },
};
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Rubik:wght@100;400;500;700&display=swap');

#app {
  font-family: 'Rubik', sans-serif;
  margin: 0;
  padding: 0;
  height: 100vh; /* Full height for background effect */
  transition: background 0.5s ease; /* Smooth transition for background */
}

/* Light theme */
.light-theme {
  --primary-bg-color: linear-gradient(135deg, #007bff 35%, #66b3ff 65%); /* Blue Gradient */
  --primary-text-color: #3C3D42; /* Text color */
  background-color: #66b3ff; /* Light blue background */
}

/* Dark theme */
.dark-theme {
  --primary-bg-color: linear-gradient(60deg, #003366 15%, #00509E 85%); /* Darker Blue Gradient */
  --primary-text-color: #F6F8E2; /* Light text color */
  background-color: #003366; /* Dark blue background */
}

body {
  background: var(--primary-bg-color);
  color: var(--primary-text-color);
  transition: background 0.5s ease;
}

.light-theme {
  background-color: #66b3ff; /* Light blue */
  color: #3C3D42; /* Dark text for light theme */
}

.dark-theme {
  background-color: #003366; /* Dark blue */
  color: #F6F8E2; /* Light text for dark theme */
}
</style>
