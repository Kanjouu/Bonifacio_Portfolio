<template>
  <div :class="currentTheme">
    <div class="profile-container">
      <!-- Left Section: Profile Image and Name -->
      <div class="left-section">
        <div class="profile-bubble">
          <div class="profile-header">
            <img class="profile-picture" src="@/assets/photo.jpg" alt="Jun L. Bonifacio" />
            <h1 class="profile-name">Jun L. Bonifacio</h1>
            <p class="profile-title">Aspiring Full-Stack Developer | Tech Enthusiast</p>
          </div>
          <div class="profile-links">
            <p><strong>GitHub:</strong> <a href="https://github.com/Kanjouu" target="_blank">https://github.com/Kanjouu</a></p>
            <p><strong>Email:</strong> <a href="mailto:mjbonifacio@tip.edu.ph">mjbonifacio@tip.edu.ph</a></p>
            <p><strong>LinkedIn:</strong> <a href="https://www.linkedin.com/in/jun-bonifacio-28263b260/" target="_blank">https://www.linkedin.com/in/jun-bonifacio-28263b260/</a></p>
          </div>
        </div>

        <!-- Aspirations Bubble -->
        <div class="aspirations-bubble">
          <h2>Future Aspirations</h2>
          <p>
            Passionate about exploring cutting-edge technologies and solving real-world problems,
            I aim to create innovative solutions that bridge the gap between technology and humanity.
          </p>
        </div>
      </div>

      <!-- Right Section: About Me and Skills -->
      <div class="right-section">
        <!-- About Me Bubble -->
        <div class="about-me-bubble">
          <h2>About Me</h2>
          <p>
            I am a Computer Engineering student currently studying at the Technological Institute of the Philippines.
            I am building my portfolio to showcase my academic journey, projects, and the skills I have developed.
          </p>
        </div>

        <!-- Skills Bubble -->
        <div class="skills-bubble">
          <h2>Skills</h2>
          <p>
            I have a solid foundation in HTML and CSS, which are fundamental for creating structured and responsive web pages. 
            These technologies allow me to craft the layout and visual design of websites, ensuring they are user-friendly and accessible. 
            My expertise in JavaScript enables me to develop interactive, dynamic, and responsive web applications. I am also proficient 
            in modern JavaScript frameworks like Vue.js, which helps me build fast, scalable, and maintainable front-end applications. 
            Beyond front-end development, I am skilled in Python, which I use for backend programming, automation tasks, and data processing. 
            With Node.js, I develop efficient server-side applications that handle high traffic and complex operations. Additionally, I have experience 
            with Firebase, utilizing its real-time database and authentication features for creating user-centered applications. 
            I am also passionate about the Internet of Things (IoT), having worked with connected devices to create intelligent systems. 
            Finally, my knowledge in cybersecurity ensures that I follow best practices to secure applications and protect sensitive data.
          </p>
        </div>

        <!-- Hobbies Bubble -->
        <div class="hobbies-bubble">
          <h2>Hobbies</h2>
          <p>
            In my free time, I enjoy a variety of activities. Music and playing instruments are a big part of my life, 
            and I find joy in creating and exploring new sounds. I am also an avid fan of sports, particularly basketball, 
            and enjoy staying active and competing. Online gaming is another passion of mine, where I connect with friends 
            and enjoy immersive gameplay. Finally, I love coding and constantly challenge myself with new projects to improve 
            my skills and learn more about technology.
          </p>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      skills: [
        'HTML & CSS',
        'JavaScript',
        'Vue.js',
        'Python',
        'Node.js',
        'Firebase',
        'IoT integrated devices',
        'Cybersecurity',
      ],
    };
  },
  computed: {
    currentTheme() {
      return this.$root.currentTheme;
    },
  },
};
</script>

<style scoped>
:root {
  --light-background: #f6f8e2;
  --dark-background: #3c3d42;
  --light-text-color: #3c3d42;
  --dark-text-color: #f6f8e2;
  --accent-color: #9ccd62;
  --highlight-color: #e0ddca;
  --highlight-text: #3c3d42;
  --contrast-text: #2a2a2a;
  --secondary-accent-color: #ff6347;
}

.profile-container {
  display: flex;
  gap: 30px;
  flex-wrap: wrap;
  padding: 20px;
  justify-content: space-between;
}

.left-section {
  width: 30%;
  display: flex;
  flex-direction: column;
  gap: 20px;
}

.profile-bubble, .aspirations-bubble, .hobbies-bubble {
  background-color: var(--light-background);
  padding: 20px;
  border-radius: 10px;
  box-shadow: 0 4px 20px rgba(0, 0, 0, 0.1);
}

.profile-header {
  text-align: center;
  margin-bottom: 20px;
}

.profile-picture {
  width: 120px;
  height: 120px;
  border-radius: 50%;
  border: 4px solid var(--accent-color);
}

.profile-name {
  font-size: 2.2rem;
  font-weight: bold;
  color: var(--contrast-text);
  margin-top: 10px;
}

.profile-title {
  font-size: 1.2rem;
  font-weight: 500;
  color: var(--secondary-accent-color);
}

.profile-links p {
  font-size: 1rem;
  color: var(--contrast-text);
}

.profile-links a {
  color: var(--accent-color);
}

.aspirations-bubble h2, .hobbies-bubble h2 {
  font-size: 1.8rem;
  color: var(--accent-color);
  margin-bottom: 10px;
  text-align: left; /* Align title to left */
}

.aspirations-bubble p, .hobbies-bubble p {
  font-size: 1rem;
  line-height: 1.6;
  color: var(--contrast-text);
  text-align: justify;
}

.right-section {
  width: 65%;
  display: flex;
  flex-direction: column;
  gap: 30px;
}

.about-me-bubble {
  background-color: var(--light-background);
  padding: 20px;
  border-radius: 10px;
  box-shadow: 0 4px 20px rgba(0, 0, 0, 0.1);
  text-align: justify;
}

.about-me-bubble h2 {
  font-size: 2rem;
  color: var(--accent-color);
  margin-bottom: 10px;
}

.about-me-bubble p {
  font-size: 1.1rem;
  color: var(--contrast-text);
  text-align: justify;
}

.skills-bubble {
  background-color: var(--light-background);
  padding: 20px;
  border-radius: 10px;
  box-shadow: 0 4px 20px rgba(0, 0, 0, 0.1);
  text-align: justify;
}

.skills-bubble h2 {
  font-size: 2rem;
  color: var(--accent-color);
  margin-bottom: 10px;
}

.skills-bubble p {
  font-size: 1.1rem;
  color: var(--contrast-text);
  text-align: justify;
}

.light-theme {
  background-color: var(--light-background);
  color: var(--light-text-color);
}

.dark-theme {
  background-color: var(--dark-background);
  color: var(--dark-text-color);
}
</style>
