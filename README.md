# Note: api keys #
APIs for Openweathermap and Geoapify were used for this project. API keys used for this notebook has been hidden. Please obtain your own API keys by following the below instructions:
## Weather API: ##
register for an account on https://home.openweathermap.org/api_keys and activate your API key via confirmation email.
## Vacation API: ##
register for an account on https://www.geoapify.com/, add a new project, and use the generated API key.

# Libraries Used #
-Matplotlib
-Pandas
-Numpy
-Requests
-Time
-Scipy
-Citipy
-Hvplot

# Overview #
This project uses latitude and longtitde to get the nearest city using citipy and the weather conditions for those cities using the Openweathermap API. That information is then used to generate the ideal cities to vacation in based on a given range of preferred temperatures and humidity. A map is generated based on the ideal vacation cities with annotation of the closest hotel within 10,000 meters by calling the geoapify API.

# WeatherPy #
A random set of 1,500 lat longs were generated using the random.uniform function in the Numpy library given the lat and long ranges (-90, 90) and (-180, 180) respectively. The lat longs were then put in a for loop to get the nearest city name for each set of lat longs using citipy library. Any repeating cities are excluded from the cities list.

The weather endpoint with city geocode was used from Openweathermap. The units were set to imperial to return data in Farenheit and format was set to JSON. The city was put in a for loop to access a variety of weather conditions for all the elements in the cities list. The results were placed in a list named city_data. The parsing of the JSON and data retrieval was put in a Try Except block because not all cities contain values for every key listed. If values for a key isn't found for a city, that city is skipped. The results are then used to create data frames, create various scatter plots, and define a function to create linear regression plots. The graphs were used to find relationships between latitudes and various weather conditions. A CSV file was saved with the resulting data frame to use in VacationPy. See Jupyter notebook for plots, result details, and analysis conclusions. 

## Weather Variables compared to Latitude: ##
-Temperature
-Humidity
-Cloudiness
-Wind speed

# VacationPy #
The CSV with cities and their weather conditions from WeatherPy is read in to create a map based on each city's latitude and longitudes on OSM tiles with each city's humidity determining the size of that city's dot. The dataframe is then filtered by my ideal temperature and humidity ranges for a vacation (75-95 degrees farenheit and 0-90% humidity respectively) and placed in a data frame named hotel_df. We then use a for loop to call the Geoapify hotel endpoint and list the closest hotel within a 10,000m radius of every city listed in the data frame. The resulting hotel is then placed in the empty "hotel" column that was created in the same row of the city. This is also put in a Try Except block so that cities with no hotel within a 10,000m radius is skipped and a "No hotel found" string is placed in that city's row. Another map is created from the data frame with that city's country and nearest hotel within a 10,000m radius added to the annotation. See Jupyter notebook for maps and details.

