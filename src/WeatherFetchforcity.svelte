<script>
    import { onMount } from 'svelte';
  
    export let city;
    export let currentTemperature;
    export let currenthumidity;
    export let currentWindSpeed;
    export let locationInfo;
    export let weatherData;
    export let errorMessage;
  
    const apiKey = '16a3974f03c4fcccc82c44efdd5a6a3f'; // Replace this with your OpenWeatherMap API key
  
    const fetchWeatherDataForCity = async () => {
      try {
        const response = await fetch(`https://api.openweathermap.org/data/2.5/forecast?q=${city}&appid=${apiKey}&units=metric`);
        if (!response.ok) {
          throw new Error('Network response was not ok');
        }
        const data = await response.json();
        weatherData = data.list;
        const { name, state, country } = data.city;
        locationInfo = state ? `Weather in ${name}, ${state}, ${country}` : `Weather in ${name}, ${country}`;
        currentTemperature = data.list[0].main.temp;
        currenthumidity = data.list[0].main.humidity;
        currentWindSpeed = data.list[0].wind.speed;
      } catch (error) {
        console.error('Error fetching weather data:', error);
        errorMessage = 'Error fetching weather data for the selected city. Please try again later.';
      }
    };
  
    onMount(fetchWeatherDataForCity);
  </script>
  
  {#if locationInfo}
    {#if weatherData}
      <div class="weather-cards">
        {#each Object.entries(weatherData) as [day, data]}
          <div class="weather-card">
            <h3 style="color: crimson;">{day}</h3>
            <p style="color: blue;">Temperature: {data.temperature}°C</p>
            <p style="color: blue;">Humidity: {data.humidity}%</p>
            <p style="color: blue;">Wind Speed: {data.windSpeed} m/s</p>
            <p style="color: blue;" >Description: {data.description}</p>
          </div>
        {/each}
      </div>
    {:else}
      <p>No weather data available</p>
    {/if}
  {:else}
    <p>Enter a city name to get weather data.</p>
  {/if}
  
  
  <style>
  
  
    .weather-cards {
    display: flex;
    justify-content: space-between;
    flex-wrap: wrap;
  
  
  }
  
  .weather-card {
    border: 1px solid #ef1313;
    border-radius: 5px;
    padding: 10px;
    margin-bottom: 20px;
    width: calc(10% - 10px);
    text-align: center;
    box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
    width: 32%;
    height: 240px;
    margin-top:20px;
    background-color:white;
   
   
  
  }
  .weather-card h3 {
    font-size: 20px;
    color: purple;
    
  }
  
  .weather-card p {
    font-size: 16px;
    color:white;
  }
  
    .weather-info {
      display: flex;
      flex-direction: column;
      margin-bottom: 38px;
      font-size: 15px;
    }
  
    .card {
      height: 100px;
      width: 180px;
      padding: 15px;
      margin-bottom: 10px;
      margin-left:-60px ;
     
      border: 1px solid #ccc;
      border-radius: 5px;
      box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
    }
    .weather-heading{
      margin-left: 700px;
    }
  
  </style>