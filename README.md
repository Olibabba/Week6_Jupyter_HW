# Week6_Jupyter_HW

## Overview
After a review of the beta version of a trip plannning app, some new features were requested. In this version we will add the current weather condition to the map of cities. The user will be able to input their ideal temperature, which will filter the map, and provide city and hotel options for their trip. The user will also be able to plan a road trip by inputting four cities they would like to travel between and getting travel itinerary plotted on Google Maps.

## Results

### Deliverable One

The first step in this project was to build a database of random cities using a random number generator to create 2000 (lat, Long) combinations. These were then matched to the nearest city using citypy. I then used the open weather API to pull the current weather conditions at each city. OF course not every city had weather data.  So out of 2000 random coordinates I built a database spanning about 750 cities, which then was further reduced to about 700 cities with wether data. These were spread across 123 countries.

It was a challenge to actually grab the current weather description because the json had the data randomly nested within a list which required some extra syntax to access the index. You can see the difference between accessing the description and the other weather data points here:
```
wind = (city_weather['wind']['speed'])
description = (city_weather['weather'][0]['description'])
```

### Deliverable Two

In this portion I asked the user for their ideal vacation temperature, and used that information to filter the list of cities. This filtered dataframe was then copied and expanded in order to store one hotel in each city. We used Google's Nearby Search API to find a hotel in as many cities as possible, however a hotel was not found in a little over 30 cities. Strangely, although the hotel column was left blank when a hotel was not found, there were no null values found. So I wen tback and refactored the try/exepct portion of the hotel finder code to fill in those blank sections with a "NaN" text:
```
    try:
        hotel_df2.loc[index, "Hotel Name"] = hotels["results"][0]["name"]
    except (IndexError):
        print("Hotel not found... skipping.")
        hotel_df2.loc[index, "Hotel Name"] = "NaN"
```
After which I located the rows containing 'NaN' and dropped them:
```
clean_hotel_df = hotel_df.drop(hotel_df[hotel_df['Hotel Name'] == 'NaN'].index).reset_index(drop=True)
```

After this delay I was please with my final map of potential destinations.
![Potential Dstinations](https://github.com/Olibabba/Week6_Jupyter_HW/blob/main/Vacation_search/WeatherPy_vacation_map.png)

### Deliverable Two


## Summary
