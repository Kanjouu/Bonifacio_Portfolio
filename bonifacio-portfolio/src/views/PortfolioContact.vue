<template>
  <div class="message-form" :class="currentTheme">
    <!-- Bubbles container under the form, covering the full screen -->
    <div class="bubbles">
      <div
        v-for="n in 100"
        :key="n"
        class="bubble"
        :style="generateBubbleStyle()"
      ></div>
    </div>

    <h2 class="form-title">LEAVE A MESSAGE</h2>
    <form @submit.prevent="submitMessage">
      <label for="user" class="form-label">User</label>
      <input type="text" id="user" v-model="user" class="form-input" required />

      <label for="message" class="form-label">Message</label>
      <textarea id="message" v-model="message" class="form-textarea" required></textarea>

      <button type="submit" class="submit-button">Submit</button>
    </form>

    <div class="contact-buttons">
      <a :href="'mailto:' + email" class="contact-button">Email Me</a>
      <a :href="facebookUrl" class="contact-button">Facebook</a>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      user: '',
      message: '',
      email: 'junbonifacio289@gmail.com', // Replace with your email
      facebookUrl: 'https://www.facebook.com/junniebae69/',
    };
  },
  computed: {
    currentTheme() {
      return this.$root.currentTheme; // Access the current theme from the root instance
    },
  },
  methods: {
    submitMessage() {
      // Logic to handle message submission can be added here
      alert(`Message from ${this.user}: ${this.message}`);
      this.user = '';
      this.message = '';
    },
    // Generate style for bubbles, using fixed positions for animation consistency
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
  },
};
</script>

<style scoped>
:root {
  --light-background: #F6F8E2;
  --dark-background: #3C3D42;
  --light-text-color: #3C3D42;
  --dark-text-color: #F6F8E2;
  --accent-color: #6272cd;
  --highlight-color: #E0DDCA;
  --highlight-text: #3C3D42;
  --contrast-text: #2A2A2A;
  --secondary-accent-color: #FF6347;
}

.light-theme {
  background-color: var(--light-background);
  color: var(--light-text-color);
}

.dark-theme {
  background-color: var(--dark-background);
  color: var(--dark-text-color);
}

.message-form {
  max-width: 600px;
  margin: 40px auto; /* Increased margin to create space from NavBar */
  padding: 30px;
  border: #3C3D42;
  border-radius: 15px;
  box-shadow: 0 6px 30px rgba(0, 0, 0, 0.2);
  transition: background-color 0.5s ease, color 0.5s ease;
  border: 2px solid var(--highlight-color); /* Border for the form */
  position: relative; /* Ensure the form content is on top of the bubbles */
  z-index: 2; /* Place form content above the bubbles */
}

.form-title {
  font-size: 2.5rem;
  font-weight: 800;
  margin-bottom: 35px;
  color: var(--accent-color);
  text-align: center;
  text-transform: uppercase;
}

.form-label {
  font-size: 1.3rem;
  font-weight: 600;
  display: block;
  border: #9CCD62;
  margin-bottom: 5px;
}

.form-input {
  width: 100%;
  padding: 12px;
  margin-bottom: 20px;
  border: 0.5px solid #1201f7; /* Border color using #9CCD62 */
  border-radius: 8px;
  font-size: 1.1rem;
  font-weight: 400;
  color: var(--contrast-text);
  background-color: transparent; /* Make background transparent for themes */
  transition: border-color 0.3s ease, box-shadow 0.3s ease;
  height: 80px; /* Set the user input field to a fixed height */
}

.form-input:focus {
  outline: none;
  border-color: var(--accent-color);
  box-shadow: 0 0 5px var(--accent-color); /* Glow effect on focus */
}

.form-textarea {
  width: 100%;
  padding: 12px;
  margin-bottom: 20px;
  border: 0.5px solid #1201f7; /* Border color using #9CCD62 */
  border-radius: 8px;
  font-size: 1.1rem;
  font-weight: 400;
  color: var(--contrast-text);
  background-color: transparent; /* Make background transparent for themes */
  transition: border-color 0.3s ease, box-shadow 0.3s ease;
  min-height: 400px; /* Make the message box longer */
}

.form-textarea:focus {
  outline: none;
  border-color: var(--accent-color);
  box-shadow: 0 0 5px var(--accent-color); /* Glow effect on focus */
}

.submit-button {
  background-color: var(--accent-color);
  color: var(--dark-text-color);
  padding: 12px 24px;
  border: 2px solid #1e05fd;
  border-radius: 15px;
  font-weight: 700;
  cursor: pointer;
  transition: background-color 0.3s ease, transform 0.3s ease;
  font-size: 1.2rem;
  display: block;
  margin: 0 auto;
}

.submit-button:hover {
  background-color: #0833f7;
  border: 1px solid #423c3d07;
  color: #3C3D42;
  transform: translateY(-3px); /* Slightly move up on hover */
  box-shadow: 0 4px 20px rgba(0, 0, 0, 0.2); /* Add shadow on hover */
}

.contact-buttons {
  display: flex;
  justify-content: space-between;
  margin-top: 20px;
}

.contact-button {
  text-decoration: none;
  color: var(--highlight-text);
  padding: 10px 15px;
  border: 2px solid var(--highlight-color);
  border-radius: 6px;
  transition: background-color 0.3s ease, color 0.3s ease, transform 0.3s ease; /* Added transform transition */
  font-weight: 600;
  flex: 1; /* Allow equal spacing */
  text-align: center; /* Center the text */
  margin: 0 5px; /* Add margin between buttons */
}

.contact-button:hover {
  background-color: #3C3D42;
  color: #021af3;
  transform: translateY(-2px); /* Slightly move up on hover */
}

/* Bubbles */
.bubbles {
  position: absolute;
  top: 0; /* Position bubbles at the top of the page */
  left: 0;
  width: 100%; /* Cover full screen width */
  height: 100vh; /* Cover the entire screen height */
  z-index: 0; /* Ensure bubbles are in the background */
  pointer-events: none; /* Disable interaction with the bubbles */
}

.bubble {
  position: absolute;
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
    transform: translateY(0); /* Start at the bottom */
    opacity: 0.8;
  }
  50% {
    opacity: 0.5;
  }
  100% {
    transform: translateY(-100vh); /* Move up out of view */
    opacity: 0;
  }
}
</style>
