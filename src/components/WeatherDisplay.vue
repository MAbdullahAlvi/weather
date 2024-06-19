<template>
  <div class="weather-display" v-if="weather">
    <h1>{{ weather.name }}</h1>
    <div class="weather-info">
      <p class="temperature">{{ weather.main.temp }} °C</p>
      <p class="description">{{ weather.weather[0].description }}</p>
    </div>

    <!-- Weather Icon -->
    <div class="weather-icon">
      <img v-if="weather.weather[0].main === 'Clouds'" src="@/assets/cloud-icon.png" alt="Cloudy">
      <img v-else-if="weather.weather[0].main === 'Clear'" src="@/assets/sun-icon.png" alt="Clear">
      <img v-else-if="weather.weather[0].main === 'Rain'" src="@/assets/rain-icon.png" alt="Rainy">
      <img v-else-if="weather.weather[0].main === 'Wind'" src="@/assets/wind-icon.png" alt="Windy">
      
    </div>
  </div>

  <div v-else class="no-data">
    <p>No weather data available. Please search for a city.</p>
  </div>
</template>

<script>
export default {
  name: 'WeatherDisplay',
  props: {
    weather: Object,
  },
};
</script>

<style scoped>
.weather-display {
  text-align: center;
  background: linear-gradient(to bottom, #4facfe, #00f2fe); /* Gradient background */
  padding: 20px;
  border-radius: 10px;
  margin: 20px auto;
  width: 80%;
  max-width: 500px;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1); /* Soft shadow */
  color: #fff; /* Text color */
  position: relative; /* Position for animation */
  overflow: hidden; /* Hide overflow for animation */
}

.weather-info {
  margin-bottom: 20px;
}

.temperature {
  font-size: 48px;
  font-weight: bold;
  margin: 10px 0;
}

.description {
  font-size: 24px;
}

.no-data {
  text-align: center;
  color: #888;
  padding: 20px;
  border-radius: 10px;
  background-color: #f0f0f0; /* Light gray background */
  margin: 20px auto;
  width: 80%;
  max-width: 500px;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1); /* Soft shadow */
}

.weather-icon img {
  max-width: 100px; /* Adjust size as needed */
  height: auto;
  margin-top: 20px; /* Adjust spacing */
  transition: transform 0.3s ease-out; /* Smooth animation */
}

.weather-icon img:hover {
  transform: scale(1.1); /* Scale up on hover */
}
</style>
