---
layout: post
title:  "Cracking the Snow Code"
description: For skiers, figuring out when the next storm is going to hit is important for having the best ski day. If given the weather information today, can we predict the amount of snow Alta will receive in 3 days?
image: /assets/img/skiing-with-a-view-min.jpg
---

# Cracking the Snow Code: Using Weather Data to Predict Alta’s Powder Days

By Brayden Humpherys

### Introduction

As a lifelong skier, I've always been fascinated by the weather patterns that dictate the quality of ski days. Planning a perfect ski trip can be challenging without knowing how much snow to expect. This project aims to predict the amount of snowfall at Alta, UT, three days in advance using historical weather data. By leveraging data science, we can make more informed decisions and enhance our skiing experiences.

![Me Skiing](%7B%7Bsite.url%7D%7D/%7B%7Bsite.baseurl%7D%7D/assets/img/smote-bar-graph.png)

### Motivation

The excitement of fresh powder days is unparalleled for any skier. However, predicting these days can be tricky. My goal is to use historical weather data to forecast snowfall, helping fellow skiers plan their trips better. This project combines my passion for skiing with my interest in data science, making it both relevant and exciting.

### Ethics

I ensured that the data collection process was ethical and legal. The data was gathered using the [Open Meteo API](https://open-meteo.com/en/docs/historical-weather-api), which provides free access to historical weather data. I adhered to the API's terms of service and followed best practices for data scraping, ensuring that the data was used responsibly and ethically.

### Data Collection

To collect the weather data, I used the Open Meteo API. Here’s a brief overview of the process:

1.  **Set Base URL and Endpoint:**

```{python}
base_url = 'https://archive-api.open-meteo.com/'
endpoint = 'v1/archive'
```

2.  **Set Parameters for 2023-2024**:

```{python}
params23_24 = {
    'latitude': 40.5888,
    'longitude': 111.6380,
    'elevation': 8560,
    'start_date': '2023-12-01',
    'end_date': '2024-03-31',
    'temperature_unit': 'fahrenheit',
    'wind_speed_unit': 'mph',
    'precipitation_unit': 'inch',
    'daily': ['weather_code','temperature_2m_max','temperature_2m_min',
               'temperature_2m_mean','apparent_temperature_max','apparent_temperature_min',
               'apparent_temperature_mean','rain_sum','snowfall_sum','precipitation_hours',
               'wind_speed_10m_max','wind_gusts_10m_max','wind_direction_10m_dominant',
               'shortwave_radiation_sum','et0_fao_evapotranspiration'],
    'timezone': 'MST'
}
```

3.  **Make API Request and Convert to JSON**:

```{python}
response23_24 = requests.get(base_url + endpoint, params=params23_24)
data23_24 = response23_24.json()
OM_23_24 = data23_24['daily']
df23_24 = pd.DataFrame(OM_23_24)
```

4.  **Repeat for 2024-2025**:

```{python}
params24_25 = {
    'latitude': 40.5888,
    'longitude': 111.6380,
    'elevation': 8560,
    'start_date': '2024-12-01',
    'end_date': '2025-02-28',
    'temperature_unit': 'fahrenheit',
    'wind_speed_unit': 'mph',
    'precipitation_unit': 'inch',
    'daily': ['weather_code','temperature_2m_max','temperature_2m_min',
               'temperature_2m_mean','apparent_temperature_max','apparent_temperature_min',
               'apparent_temperature_mean','rain_sum','snowfall_sum','precipitation_hours',
               'wind_speed_10m_max','wind_gusts_10m_max','wind_direction_10m_dominant',
               'shortwave_radiation_sum','et0_fao_evapotranspiration'],
    'timezone': 'MST'
}
response24_25 = requests.get(base_url + endpoint, params=params24_25)
data24_25 = response24_25.json()
OM_24_25 = data24_25['daily']
df24_25 = pd.DataFrame(OM_24_25)
```

5.  **Combine DataFrames and Create 3-Day Snowfall Prediction**:

```{python}
df23_25 = pd.concat([df23_24, df24_25], ignore_index=True)
df23_25['3day_prediction'] = df23_25['snowfall_sum'].shift(-3)
df23_25 = df23_25.iloc[:-3,:]  # Remove last 3 rows with NaN values
```

6.  **Save Combined Data to CSV**:

```{python}
df23_25.to_csv('SnowFall23_25.csv', index=False)
```

#### Exploratory Data Analysis (EDA)

To understand the data better, I performed some exploratory data analysis (EDA). Here are a few highlights:

1.  **Snowfall by Month**

![Snowfall by Month]()

2.  **Snowfall by Minimum Temperature**

![Snowfall by Min Temp]()

### Dataset Summary

-   Shape: 209 observations by 18 variables.

-   Variables: Weather code, max/min/mean temperature, max/min/mean 'feels-like' temperature, rain sum, snowfall sum, precipitation hours, max wind speed, max wind gusts, wind direction, radiation sum, evapotranspiration, 3-day snowfall prediction.

### Conclusion

Having successfully collected and analyzed the historical weather data, the next step in this project is to build a predictive model for snowfall at Alta, UT. This model will help skiers plan their trips more effectively by forecasting snowfall three days in advance. If you're interested in following along or replicating this project, please visit my [GitHub repository](https://github.com/BraydenHumpherys/Snowfall-Prediction) for the code and data. Your feedback and contributions are welcome!
