# real-time-weather-dashboard
import React, { useState } from 'react';
import axios from 'axios';

function App() {
  const [city, setCity] = useState('');
  const [weather, setWeather] = useState(null);

  const getWeather = async () => {
    if (!city) return;
    const res = await axios.get(`http://localhost:5000/weather?city=${city}`);
    setWeather(res.data);
  };

  return (
    <div style={{ padding: 20, fontFamily: 'Arial' }}>
      <h2>🌤️ Real-Time Weather Dashboard</h2>
      <input
        type="text"
        value={city}
        placeholder="Enter city"
        onChange={(e) => setCity(e.target.value)}
      />
      <button onClick={getWeather}>Get Weather</button>

      {weather && (
        <div style={{ marginTop: 20 }}>
          <h3>Weather in {weather.name}</h3>
          <p>🌡️ Temperature: {weather.main.temp}°C</p>
          <p>💧 Humidity: {weather.main.humidity}%</p>
          <p>🌬️ Wind: {weather.wind.speed} m/s</p>
        </div>
      )}
    </div>
  );
}

export default App;
