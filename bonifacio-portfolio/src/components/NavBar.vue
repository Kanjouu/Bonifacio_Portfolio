<template>
  <nav class="navbar navbar-expand-lg navbar-custom" :style="{ backgroundColor: currentBackgroundColor }">
    <button class="navbar-toggler" type="button" data-toggle="collapse" data-target="#navbarNav" aria-controls="navbarNav" aria-expanded="false" aria-label="Toggle navigation">
      <span class="navbar-toggler-icon"></span>
    </button>
    <div class="collapse navbar-collapse" id="navbarNav">
      <ul class="navbar-nav mx-auto">
        <li class="nav-item" v-for="(link, index) in navLinks" :key="index">
          <router-link
            class="nav-link"
            :to="link.href"
            :class="{ 'nav-link-hover': true, 'nav-link-active': $route.path === link.href }"
          >
            {{ link.text }}
          </router-link>
        </li>
      </ul>
    </div>
  </nav>
</template>

<script>
export default {
  name: 'NavBar',
  data() {
    return {
      navLinks: [
        { text: 'Login', href: '/login' },
        { text: 'Profile', href: '/portfolio/profile' },
        { text: 'Showcase', href: '/portfolio/showcase' },
        { text: 'Creative', href: '/portfolio/creative' },
        { text: 'Contact', href: '/portfolio/contact' }
      ]
    };
  },
  computed: {
    currentBackgroundColor() {
      return this.$root.currentTheme === 'light-theme' ? '#007BFF' : '#0056B3';
    },
    currentLinkColor() {
      return this.$root.currentTheme === 'light-theme' ? '#FFFFFF' : '#E0E0E0';
    },
  }
};
</script>

<style scoped>
/* Navbar container styles */
.navbar {
  border-radius: 30px;
  padding: 10px 30px;
  box-shadow: 0 4px 10px rgba(0, 0, 0, 0.2);
  margin-top: 20px;
  transition: background-color 0.3s ease, color 0.3s ease, box-shadow 0.3s ease;
}

/* Navbar link styles */
.navbar-nav .nav-link {
  font-size: 1.25rem;
  margin: 0 15px;
  border-radius: 5px;
  padding: 5px 10px;
  color: inherit;
  transition: background-color 0.3s ease, color 0.3s ease, transform 0.2s ease;
}

/* Hover effect for light and dark themes */
.navbar-nav .nav-link-hover:hover {
  background-color: #0056B3;
  color: #FFFFFF;
  transform: scale(1.1); /* Subtle zoom effect on hover */
}

/* Active state effect */
.navbar-nav .nav-link-active {
  background-color: #003F7F;
  color: #FFFFFF;
  transform: scale(1.05); /* Slight zoom effect when active */
}

/* Active state when link is clicked */
.navbar-nav .nav-link:active {
  transform: scale(0.98); /* Slight shrink effect on click */
}

/* Light theme */
.light-theme .navbar {
  background-color: #007BFF;
}

.light-theme .nav-link {
  color: #FFFFFF;
}

/* Dark theme */
.dark-theme .navbar {
  background-color: #0056B3;
}

.dark-theme .nav-link {
  color: #E0E0E0;
}

.dark-theme .nav-link-hover:hover {
  background-color: #003F7F;
}
</style>
