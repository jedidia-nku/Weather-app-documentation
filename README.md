# Weather App Documentation

## Table of Contents

1. [Introduction](#introduction)
2. [Project Functionality](#project-functionality)
3. [API Usage](#api-usage)
   - [OpenWeatherMap API](#openweathermap-api)
   - [Google Maps API](#google-maps-api)
4. [Technical Details](#technical-details)
   - [Frontend](#frontend)
   - [Backend](#backend)
   - [Environment Variables](#environment-variables)
5. [Installation and Setup](#installation-and-setup)
6. [Usage](#usage)

---

## Introduction

The **Weather App** is a modern web application designed to provide users with real-time weather updates for any location. Built using **React.js**, **Next.js**, and **Tailwind CSS**, the app integrates with **OpenWeatherMap API** for weather data and **Google Maps API** for location services. It offers a user-friendly interface that works seamlessly across all devices, ensuring a smooth and responsive experience.

---

## Project Functionality

### Key Features:

- **Search Weather by Location**: Users can search for weather updates by city name or current location.
- **Real-time Weather Data**: The app fetches and displays current temperature, weather conditions, humidity, wind speed, and more.
- **Interactive Map**: The Google Maps API is used to display the current location of the user or searched city on an interactive map.
- **Mobile-friendly UI**: Designed to adapt across all devices, making it easy to use on both mobile and desktop.

---

## API Usage

### OpenWeatherMap API

**Endpoint**: The app uses the **Current Weather Data** API from OpenWeatherMap to fetch real-time weather information.

#### How It Works:
1. The app sends an HTTP request to the OpenWeatherMap API using the city name (or geographic coordinates if using current location).
2. The API returns a JSON object containing weather data, including:
   - Current temperature
   - Weather conditions (clear, cloudy, rainy, etc.)
   - Wind speed
   - Humidity
   - Sunrise and sunset times
   - Weather icons representing conditions visually

#### Example Request:

https://api.openweathermap.org/data/2.5/weather?q=London&appid={OPENWEATHERMAP_API_KEY}&units=metric

### API Response (Sample):


{
  "main": {
    "temp": 15.5,
    "humidity": 72
  },
  "weather": [
    {
      "description": "clear sky",
      "icon": "01d"
    }
  ],
  "wind": {
    "speed": 3.5
  },
  "sys": {
    "sunrise": 1629886400,
    "sunset": 1629936000
  },
  "name": "London",
  "coord": {
    "lat": 51.5074,
    "lon": -0.1278
  }
}


#### Parameters:
- **`q`**: City name or coordinates (latitude, longitude)
- **`appid`**: Your unique API key
- **`units`**: Set to metric for temperature in Celsius

### Google Maps API

The Google Maps API is used to display an interactive map showing the user’s location or the city they searched for.

#### How It Works:
1. Upon user search or location detection, the latitude and longitude of the city are passed to the Google Maps API.
2. The API renders a map centered around the provided coordinates, marking the location with a pin.

#### API Key Requirements:
- **Google Maps JavaScript API** must be enabled in your Google Cloud Console.
- The map is embedded using the `GoogleMap` component, passing latitude and longitude coordinates.

#### Example Integration:

<GoogleMap
  center={{ lat: 51.5074, lng: -0.1278 }}
  zoom={10}
  mapContainerStyle={{ width: '100%', height: '400px' }}
/>

## Technical Details

### Frontend

- **React.js**: The core JavaScript library used to build the dynamic user interface.
- **Next.js**: Enables server-side rendering (SSR) and static site generation (SSG), improving performance and SEO.
- **Tailwind CSS**: Provides utility-first CSS classes for rapid UI development.
  
#### Important Components:
1. **Search Component**: Handles user input and triggers API requests based on the city name or current location.
2. **Weather Display Component**: Receives data from OpenWeatherMap API and displays it in a clean, responsive layout.
3. **Google Maps Integration**: Uses `@react-google-maps/api` for embedding an interactive map that updates based on the user's location or search.

### Backend

- **Next.js API Routes**: API routes in Next.js are used to proxy requests to OpenWeatherMap and Google Maps APIs. This ensures that API keys are kept secure and not exposed on the client side.

Example API Route for fetching weather data:

export default async function handler(req, res) {
  const { city } = req.query;
  const response = await fetch(`https://api.openweathermap.org/data/2.5/weather?q=${city}&appid=${process.env.NEXT_PUBLIC_WEATHER_API_KEY}&units=metric`);
  const data = await response.json();
  res.status(200).json(data);
}

### Environment Variables

The app uses environment variables to store sensitive API keys.

Create a `.env.local` file in the root directory of your project and add the following:


OPENWEATHERMAP_API_KEY = eb3722bea7fd087191effcf2ba81810a


## Installation and Setup

1. Clone the repository:

   git clone https://github.com/jedidia-nku/weather-app.git


2. Navigate to the project directory:
   
   cd weather-app
   

2. Install dependencies:
   
    npm install
    

2. Add your API keys to .env.local file:
   
OPENWEATHERMAP_API_KEY = eb3722bea7fd087191effcf2ba81810a


2. Start the development server:
   
   npm run dev
6. Open http://localhost:3000 in your browser to view the app.

