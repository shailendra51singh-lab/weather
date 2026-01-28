<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Current Weather Status</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      background: linear-gradient(135deg, #74ebd5, #9face6);
      min-height: 100vh;
      display: flex;
      align-items: center;
      justify-content: center;
      margin: 0;
    }
    .weather-card {
      background: #fff;
      padding: 25px 30px;
      border-radius: 12px;
      width: 320px;
      text-align: center;
      box-shadow: 0 10px 25px rgba(0,0,0,0.15);
    }
    .weather-card h1 {
      margin-bottom: 15px;
      font-size: 22px;
    }
    input {
      width: 100%;
      padding: 10px;
      border-radius: 6px;
      border: 1px solid #ccc;
      margin-bottom: 10px;
      font-size: 14px;
    }
    button {
      width: 100%;
      padding: 10px;
      border: none;
      border-radius: 6px;
      background: #4a6cf7;
      color: #fff;
      font-size: 15px;
      cursor: pointer;
    }
    button:hover {
      background: #3b5be0;
    }
    .result {
      margin-top: 20px;
    }
    .temp {
      font-size: 36px;
      font-weight: bold;
    }
    .status {
      font-size: 18px;
      text-transform: capitalize;
    }
    .error {
      color: red;
      margin-top: 10px;
    }
  </style>
</head>
<body>
  <div class="weather-card">
    <h1>Current Weather</h1>
    <input type="text" id="city" placeholder="Enter city name" />
    <button onclick="getWeather()">Check Weather</button>

    <div class="result" id="result"></div>
  </div>

  <script>
    const apiKey = "YOUR_API_KEY_HERE"; // OpenWeatherMap API key

    function getWeather() {
      const city = document.getElementById("city").value;
      const result = document.getElementById("result");

      if (city === "") {
        result.innerHTML = '<div class="error">Please enter a city name</div>';
        return;
      }

      fetch(`https://api.openweathermap.org/data/2.5/weather?q=${city}&appid=${apiKey}&units=metric`)
        .then(response => response.json())
        .then(data => {
          if (data.cod !== 200) {
            result.innerHTML = '<div class="error">City not found</div>';
            return;
          }

          result.innerHTML = `
            <div class="temp">${data.main.temp}°C</div>
            <div class="status">${data.weather[0].description}</div>
            <div>Humidity: ${data.main.humidity}%</div>
            <div>Wind Speed: ${data.wind.speed} m/s</div>
          `;
        })
        .catch(() => {
          result.innerHTML = '<div class="error">Unable to fetch weather data</div>';
        });
    }
  </script>
</body>
</html>

