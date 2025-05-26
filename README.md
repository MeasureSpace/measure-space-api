# Measure Space API Python Package

A Python package for accessing weather, climate, air quality, and geocoding APIs provided by [MeasureSpace.io](https://measurespace.io).

## Features

- Get hourly and daily weather forecasts
- Get daily climate forecasts
- Get hourly and daily air quality forecasts
- Geocoding: convert city names to coordinates and vice versa
- Unified API call interface with flexible parameters

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

Import the package and call the functions:

```python
from measure_space_api.main import (
    get_hourly_weather, get_daily_weather, get_daily_climate,
    get_hourly_air_quality, get_daily_air_quality,
    get_lat_lon_from_city, get_city_from_lat_lon
)

# Example: Get hourly weather by coordinates
api_key = "YOUR_API_KEY"
df = get_hourly_weather(api_key, latitude=40.2, longitude=110.2, return_json=False)
print(df.head())

# Example: Get daily weather by city name
geocoding_api_key = "YOUR_GEOCODING_API_KEY"
df = get_daily_weather(api_key, geocoding_api_key, location_name="Beijing", return_json=False)
print(df.head())
```

## API Functions

### Weather

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

## Example: Get City Coordinates

```python
from measure_space_api.main import get_lat_lon_from_city
lat, lon = get_lat_lon_from_city(geocoding_api_key, "Shanghai")
print(lat, lon)
```

## Environment Variables

You may use a `.env` file to store your API keys and load them with `python-dotenv`.

```env
HOURLY_WEATHER_API_KEY=your_key
HOURLY_WEATHER_API_URL=https://api.example.com/hourly
GEOCODING_API_KEY=your_geocoding_key
GEOCODING_API_URL=https://api.example.com/geocode
```

## API Documentation

- See [MeasureSpace API Explorer](https://measurespace.io/api-explorer) for details on endpoints and parameters.
- See [MeasureSpace Documentation](https://measurespace.io/documentation) for variable names and meanings.

## License

Apache License
