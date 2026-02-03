# Air Quality API

REST API for real-time air quality index (AQI) and pollutant data. Query by city name or GPS coordinates.

## Features

- Two endpoints: city name or lat/lon coordinates
- Returns AQI + 6 major pollutants (PM2.5, PM10, O₃, NO₂, SO₂, CO)
- Real-time data from global monitoring networks
- 5,000 requests/month on free tier
- Example Response:
```json
{
  "air_quality_index": 85,
  "PM2.5": { "concentration": 4.72, "aqi": 15 },
  "PM10": { "concentration": 5.9, "aqi": 5 },
  "ozone": { "concentration": 70.32, "aqi": 85 },
  "nitrogen_dioxide": { "concentration": 12.09, "aqi": 15 },
  "sulfur_dioxide": { "concentration": 6.92, "aqi": 10 },
  "carbon_monoxide": { "concentration": 222.07, "aqi": 2 }
}
```

## Authentication

1. Create account at [omkar.cloud](https://www.omkar.cloud/auth/sign-up)

![Sign Up](https://raw.githubusercontent.com/omkarcloud/assets/master/images/signup.png)

2. Get API key from [omkar.cloud/api-key](https://www.omkar.cloud/api-key)

![Copy API Key](https://raw.githubusercontent.com/omkarcloud/assets/master/images/enrichment-key-omkar.png)

3. Include `API-Key` header in requests

## Quick Start

```bash
curl -X GET "https://air-quality-api.omkar.cloud/air-quality/city?city=New%20York" \
  -H "API-Key: YOUR_API_KEY"
```

```json
{
  "air_quality_index": 85,
  "PM2.5": { "concentration": 4.72, "aqi": 15 },
  "ozone": { "concentration": 70.32, "aqi": 85 }
}
```

## Installation

### Python

```bash
pip install requests
```

```python
import requests

response = requests.get(
    "https://air-quality-api.omkar.cloud/air-quality/city",
    params={"city": "New York"},
    headers={"API-Key": "YOUR_API_KEY"}
)

data = response.json()
print(f"AQI: {data['air_quality_index']}")
```

### Node.js

```bash
npm install axios
```

```javascript
import axios from "axios";

const response = await axios.get("https://air-quality-api.omkar.cloud/air-quality/city", {
    params: { city: "New York" },
    headers: { "API-Key": "YOUR_API_KEY" }
});

console.log(`AQI: ${response.data.air_quality_index}`);
```

## API Reference

### Endpoints

```
GET https://air-quality-api.omkar.cloud/air-quality/city
GET https://air-quality-api.omkar.cloud/air-quality/coords
```

### Headers

| Header | Required | Description |
|--------|----------|-------------|
| `API-Key` | Yes | API key from [omkar.cloud/api-key](https://www.omkar.cloud/api-key) |

### Parameters (City Endpoint)

| Parameter | Required | Description |
|-----------|----------|-------------|
| `city` | Yes | City name (e.g., "New York", "London") |

### Parameters (Coords Endpoint)

| Parameter | Required | Description |
|-----------|----------|-------------|
| `lat` | Yes | Latitude (-90 to 90) |
| `lon` | Yes | Longitude (-180 to 180) |

### Response Fields

| Field | Type | Description |
|-------|------|-------------|
| `air_quality_index` | number | Overall AQI (0-500 scale) |
| `PM2.5` | object | Fine particles (<2.5μm) |
| `PM10` | object | Coarse particles (<10μm) |
| `ozone` | object | Ground-level ozone (O₃) |
| `nitrogen_dioxide` | object | NO₂ from combustion |
| `sulfur_dioxide` | object | SO₂ from industrial sources |
| `carbon_monoxide` | object | CO from incomplete combustion |

Each pollutant object contains:
- `concentration` — Measured value (μg/m³)
- `aqi` — Individual AQI for that pollutant

### AQI Scale

| Range | Level | Meaning |
|-------|-------|---------|
| 0-50 | Good | Safe for everyone |
| 51-100 | Moderate | Acceptable |
| 101-150 | Unhealthy (Sensitive) | Limit outdoor activity if sensitive |
| 151-200 | Unhealthy | Everyone may feel effects |
| 201-300 | Very Unhealthy | Health alert |
| 301-500 | Hazardous | Emergency conditions |

## Examples

### Get AQI by city name

```python
response = requests.get(
    "https://air-quality-api.omkar.cloud/air-quality/city",
    params={"city": "Tokyo"},
    headers={"API-Key": "YOUR_API_KEY"}
)

aqi = response.json()["air_quality_index"]
print(f"Tokyo AQI: {aqi}")
```

### Get AQI by coordinates

```python
response = requests.get(
    "https://air-quality-api.omkar.cloud/air-quality/coords",
    params={"lat": 51.5074, "lon": -0.1278},
    headers={"API-Key": "YOUR_API_KEY"}
)

data = response.json()
print(f"London AQI: {data['air_quality_index']}")
```


## Error Handling

```python
response = requests.get(
    "https://air-quality-api.omkar.cloud/air-quality/city",
    params={"city": "InvalidCity123"},
    headers={"API-Key": "YOUR_API_KEY"}
)

if response.status_code == 200:
    data = response.json()
elif response.status_code == 401:
    # Invalid API key
    pass
elif response.status_code == 429:
    # Rate limit exceeded
    pass
```

## Rate Limits

| Plan | Price | Requests/Month |
|------|-------|----------------|
| Free | $0 | 5,000 |
| Starter | $25 | 100,000 |
| Grow | $75 | 1,000,000 |
| Scale | $150 | 10,000,000 |

## Questions? We have answers.

Reach out anytime. We will solve your query within 1 working day.

[![Contact Us on WhatsApp about Air Quality API](https://raw.githubusercontent.com/omkarcloud/assets/master/images/whatsapp-us.png)](https://api.whatsapp.com/send?phone=918178804274&text=I%20have%20a%20question%20about%20the%20Air%20Quality%20API.)

[![Contact Us on Email about Air Quality API](https://raw.githubusercontent.com/omkarcloud/assets/master/images/ask-on-email.png)](mailto:happy.to.help@omkar.cloud?subject=Air%20Quality%20API%20Question)
