<template>
  <div :class="currentTheme">
    <div class="showcase-container">
      <h1 class="showcase-title">My Projects</h1>
      <div class="video-grid">
        <div v-for="(video, index) in videos" :key="index" class="video-card">
          <video
            :src="video.src"
            controls
            muted
            class="video-thumbnail"
            @mouseover="playVideo(video)"
            @mouseleave="pauseVideo(video)"
          ></video>
          <h2 class="video-title">{{ video.title }}</h2>
          <p class="video-description">{{ video.description }}</p>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      videos: [
        {
          title: "Project 1: Compedia",
          description:
            "This project is about making a database for soft copies of research papers for TIPians.",
          src: require('@/assets/vid1.mp4'),
        },
        {
          title: "Project 2: Sensor Integration and Data Visualization",
          description:
            "This project is about connecting a DHT11 to NodeMcu and to send real sensor readings such as temperature and humidity levels.",
          src: require('@/assets/vid2.mp4'),
        },
        {
          title: "Project 3: Simple Voltmeter",
          description:
            "This project allows users to contorl the voltage and the result will be shown in the LCD and will state if the label is low, medium, or high.",
          src: require('@/assets/vid3.mp4'),
        },
      ],
    };
  },
  computed: {
    currentTheme() {
      return this.$root.currentTheme;
    },
  },
  methods: {
    playVideo(video) {
      const videoElement = document.querySelector(`video[src="${video.src}"]`);
      videoElement.play();
    },
    pauseVideo(video) {
      const videoElement = document.querySelector(`video[src="${video.src}"]`);
      videoElement.pause();
    },
  },
};
</script>

<style scoped>
.showcase-container {
  text-align: center;
  padding: 50px 20px;
  background: linear-gradient(135deg, #036cf5 0%, #e0ddca 100%); /* Soft gradient */
  box-shadow: 0 4px 20px rgba(0, 0, 0, 0.1);
  border-radius: 15px;
  font-family: 'Rubik', sans-serif; /* Rubik font */
}

.showcase-title {
  font-size: 3em;
  color: #3c3d42;
  margin-bottom: 40px;
  font-weight: bold;
  text-shadow: 1px 1px 2px rgba(0, 0, 0, 0.2);
}

.video-grid {
  display: flex;
  flex-wrap: wrap;
  justify-content: center; /* Center the items */
  gap: 30px;
}

.video-card {
  background-color: #ffffff;
  border: 2px solid #007bff; /* Blue border for the card */
  border-radius: 15px;
  overflow: hidden;
  transition: transform 0.3s, box-shadow 0.3s;
  box-shadow: 0 2px 15px rgba(0, 0, 0, 0.1);
  width: 350px; /* Set width for the card */
  height: auto; /* Let the height adjust based on the content */
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: flex-start;
}

.video-card:hover {
  transform: translateY(-8px);
  box-shadow: 0 8px 25px rgba(0, 0, 0, 0.2);
}

.video-thumbnail {
  width: 100%;
  height: auto;
  border-bottom: 4px solid #007bff; /* Blue border for the video thumbnail */
}

.video-title {
  font-size: 1.4em;
  color: #3c3d42;
  margin: 15px 0 10px;
  font-weight: bold;
}

.video-description {
  color: #6c757d;
  padding: 0 15px 20px;
  font-size: 1em;
  line-height: 1.5;
}
</style>
