<template>
  <div id="app">
    <div class="background-image"></div>
    <div class="content">
      <h1 class="app-title">Weather Forecast</h1>
      <SearchBar @search="fetchWeather"></SearchBar>
      <WeatherDisplay :weather="weatherData"></WeatherDisplay>
      <div v-if="loading" class="loading-indicator">
        <div class="spinner"></div>
        <p>Loading...</p>
      </div>
      <div v-if="error" class="error-message">
        <p>{{ errorMessage }}</p>
      </div>
    </div>
  </div>
</template>

<script>
import SearchBar from './components/SearchBar.vue';
import WeatherDisplay from './components/WeatherDisplay.vue';
import axios from 'axios';

export default {
  name: 'App',
  components: {
    SearchBar,
    WeatherDisplay,
  },
  data() {
    return {
      weatherData: null,
      loading: false,
      error: false,
      errorMessage: '',
    };
  },
  methods: {
    async fetchWeather(city) {
      this.loading = true;
      try {
        const apiKey = '30d4741c779ba94c470ca1f63045390a';
        const response = await axios.get(`https://api.openweathermap.org/data/2.5/weather?q=${city}&appid=${apiKey}&units=metric`);
        this.weatherData = response.data;
        this.error = false;
      } catch (error) {
        console.error(error);
        this.errorMessage = 'Weather data not found. Please try again.';
        this.error = true;
        this.weatherData = null;
      } finally {
        this.loading = false;
      }
    },
  },
};
</script>

<style>
#app {
  position: relative;
  height: 100vh;
  overflow: hidden;
}

.background-image {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  z-index: -1;
  background-image: url('@/assets/background.png'); /* Replace with your background image path */
  background-size: cover;
  background-position: center;
  filter: brightness(0.6); /* Adjust brightness for readability */
}

.content {
  position: relative;
  z-index: 1;
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
  height: 100%;
  font-family: 'Roboto', Arial, sans-serif;
  color: #fff;
}

.app-title {
  font-size: 3rem;
  margin-top: 50px;
  animation: fadeIn 1s ease-out; /* Fade-in animation for title */
}

@keyframes fadeIn {
  0% { opacity: 0; transform: translateY(-20px); }
  100% { opacity: 1; transform: translateY(0); }
}

.loading-indicator {
  display: flex;
  align-items: center;
  justify-content: center;
  margin-top: 20px;
  animation: fadeInUp 0.5s ease-out; /* Fade-in animation with slight upward movement */
}

@keyframes fadeInUp {
  0% { opacity: 0; transform: translateY(20px); }
  100% { opacity: 1; transform: translateY(0); }
}

.spinner {
  border: 4px solid rgba(255, 255, 255, 0.1);
  border-top: 4px solid #4facfe; /* Blue spinner color */
  border-radius: 50%;
  width: 30px;
  height: 30px;
  animation: spin 1s linear infinite;
}

@keyframes spin {
  0% { transform: rotate(0deg); }
  100% { transform: rotate(360deg); }
}

.error-message {
  background-color: rgba(255, 0, 0, 0.6); /* Semi-transparent red background */
  color: #fff; /* White text color */
  padding: 10px;
  border-radius: 5px;
  margin-top: 20px;
  max-width: 80%;
  text-align: center;
  animation: slideInDown 0.5s ease-out; /* Slide-in animation from top */
}

@keyframes slideInDown {
  0% { opacity: 0; transform: translateY(-100%); }
  100% { opacity: 1; transform: translateY(0); }
}
</style>
