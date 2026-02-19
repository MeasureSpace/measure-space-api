# Measure Space API Python Package

A Python package for accessing weather, climate, air quality, agriculture, pollen, and geocoding APIs provided by [MeasureSpace.io](https://measurespace.io).

## Features

Global Hourly Weather Forecast
- 5-day forecast at hourly frequency and global scale
- over 20 common weather variables with timezone and weather icons
- available at local and UTC time
- imperial and metric units
- support agriculture, logistics, IoT and many other general weather applications

Global Daily Weather Forecast
- 15-day forecast at daily frequency and global scale
- over 30 common weather variables with timezone, sunrise, sunset and weather icons
- available at local and UTC time
- daytime and nighttime aggregations
- imperial and metric units
- support agriculture, logistics, IoT and many other general weather applications

Global Climate Forecast
- 10-month forecast at daily frequency and global scale
- 11 common variables
- imperial and metric units
- support agriculture and many other general climate applications

Global Air Quality Forecast
- 5-day air quality forecast at hourly and daily frequency and global scale
- 7 common air pollutants including Air Quality Index
- help people plan outdoor activities and make health product marketing more efficient

Global City Geocoding
- dedicated to city geocoding and reverse geocoding
- autocomplete for more than 200,000 cities from 245 countries
- get matched cities based on user inputs
- convert city names to corresponding latitude and longitude info
- find nearest city based on latitude and longitude
- live demo through our weather dashboard search city feature

Agriculture
- growing degree days forecast
- growth stage forecast
- heat stress forecast
- frost stress forecast
- data from past year to next 9 months
- imperial and metric units
- support major crops like corn, soybean, wheat, rice and many others

Global Pollen Forecast
- 10-day pollen forecast at daily frequency and global scale
- 3 common pollen types
- help people plan outdoor activities and make health product marketing more efficient

## Installation

Clone the repository and install dependencies:

```bash
pip install -e .
```

Or install from PyPI:

```bash
pip install measure-space-api
```

## Usage

### Get Weather, Climate, Air Quality, Agriculture and Pollen Variables

Import the package and call the functions:

```python
from measure_space_api import (
    get_hourly_weather, get_daily_weather, get_daily_climate,
    get_hourly_air_quality, get_daily_air_quality,
    get_lat_lon_from_city, get_city_from_lat_lon
)

# Example: Get hourly weather by coordinates
api_key = "YOUR_API_KEY"
params = {
    # Variable names and meaning can be found at https://measurespace.io/documentation#global-hourly-weather-forecast-variables
    "variables": "tp,t2m",
    "unit": "metric"
}
df = get_hourly_weather(api_key, latitude=40.2, longitude=110.2, params=params, return_json=False)
print(df.head())

# Example: Get hourly weather by city name
geocoding_api_key = "YOUR_GEOCODING_API_KEY"
df = get_hourly_weather(api_key, geocoding_api_key, location_name="Beijing", params=params, return_json=False)
print(df.head())

# Example: get metadata (variable description, unit)
get_metadata('tp', unit='metric')
```

### Get City Coordinates

```python
from measure_space_api.main import get_lat_lon_from_city
lat, lon = get_lat_lon_from_city(geocoding_api_key, "Shanghai")
print(lat, lon)
```

### Use Environment Variables

You may use a `.env` file to store your API keys and load them with `python-dotenv`.

```env
HOURLY_WEATHER_API_KEY=your_hourly_weather_key
DAILY_WEATHER_API_KEY=your_daily_weather_key
DAILY_CLIMATE_API_KEY=your_daily_climate_key
AIR_QUALITY_API_KEY=your_air_quality_key
GEOCODING_API_KEY=your_geocoding_key
```

Call API using API keys from `.env` file.

```python
from measure_space_api import (
    get_hourly_weather, get_daily_weather, get_daily_climate,
    get_hourly_air_quality, get_daily_air_quality,
    get_lat_lon_from_city, get_city_from_lat_lon
)
from dotenv import load_dotenv
import os

# Load environment variables from .env file
load_dotenv()
# Example: Get hourly weather by coordinates
params = {
    # Variable names and meaning can be found at https://measurespace.io/documentation#global-hourly-weather-forecast-variables
    "variables": "tp,t2m",
    "unit": "metric"
}
df = get_hourly_weather(HOURLY_WEATHER_API_KEY, latitude=40.2, longitude=110.2, params=params, return_json=False)
print(df.head())

```

## API Functions

### Weather and Climate

- `get_hourly_weather(api_key, geocoding_api_key=None, location_name=None, latitude=None, longitude=None, params={'variables': 'tp, t2m', 'unit': 'metric'}, return_json=True)`
- `get_daily_weather(api_key, geocoding_api_key=None, location_name=None, latitude=None, longitude=None, params={'variables': 'tp, minT, maxT', 'unit': 'metric'}, return_json=True)`
- `get_daily_climate(api_key, geocoding_api_key=None, location_name=None, latitude=None, longitude=None, params={'variables': 'tp, tmin, tmax', 'unit': 'metric'}, return_json=True)`

### Air Quality

- `get_hourly_air_quality(api_key, geocoding_api_key=None, location_name=None, latitude=None, longitude=None, params={'variables': 'AQI, DP'}, return_json=True)`
- `get_daily_air_quality(api_key, geocoding_api_key=None, location_name=None, latitude=None, longitude=None, params={'variables': 'AQI'}, return_json=True)`

### Geocoding

- `get_lat_lon_from_city(api_key, location_name)`
- `get_city_from_lat_lon(api_key, latitude, longitude)`

## Parameters

- `api_key`: Your API key for the weather/climate/air quality service
- `geocoding_api_key`: (Optional) API key for geocoding service
- `location_name`: (Optional) City name (e.g., "New York", "Beijing, China")
- `latitude`, `longitude`: (Optional) Coordinates
- `params`: (Optional) Dictionary of additional API parameters (e.g., variables, units, local_flag)
- `return_json`: If True, returns JSON; if False, returns a pandas DataFrame

## API Documentation

- See [MeasureSpace API Explorer](https://measurespace.io/api-explorer) for details on endpoints and parameters.
- See [MeasureSpace Documentation](https://measurespace.io/documentation) for variable names and meanings.

## Publish to PyPI

- `uv build`
- `uv publish --token <your-pypi-token>`

## License

Apache License
