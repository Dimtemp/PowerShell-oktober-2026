# 5 Using Data from REST APIs

Many modern applications provide data via REST APIs. You will learn:
- How to call APIs using Invoke-RestMethod.
- Processing JSON data and converting it into usable objects.

Example: Retrieving data from a web API.

# Representational state transfer (REST)
## Note! In this exercise we rely on external APIs and information sources. There is no guarantee that these services are currently available, or work as expected.

Representational state transfer (REST) is a software architectural style that defines a set of constraints to be used for creating Web services. Web services that conform to the REST architectural style, called RESTful Web services, provide interoperability between computer systems on the internet. RESTful Web services allow the requesting systems to access and manipulate textual representations of Web resources by using a uniform and predefined set of stateless operations. 


## Task: Spot the International Space Station (ISS)
1. Enter this command to store a URL in a variable: ```$url = 'https://api.wheretheiss.at/v1/satellites/25544'```
1. Since the service offers data in JSON, we can use the Invoke-RestMethod command to retrieve data: ```Invoke-RestMethod $url```
1. Notice the visibility property. Eclipsed means you cannot see the ISS at this moment. If it displays 'daylight' it means you might be able to see it, but it will be very faint.
1. Select the relevant information: ```$r | Select-Object latitude, longitude, altitude, velocity, visibility```
1. You can optionally visit the corresponding website to visualize the location of the ISS. This should correspond to the visibility property from the previous command: ```https://wheretheiss.at/```


## Task: Explore a 7Timer! weather forecast
1. Store the URL for a forecast near Amsterdam in a variable: ```$url = 'http://www.7timer.info/bin/api.pl?lon=4&lat=52&product=civil&output=json'```
1. Retrieve the JSON response as a PowerShell object: ```$r = Invoke-RestMethod $url```
1. Inspect the response: ```$r```
1. The forecast entries are in the dataseries property. Inspect the first entry: ```$r.dataseries[0]```
1. Display the forecast time, weather condition, temperature, and wind: ```$r.dataseries | Select-Object timepoint, weather, temp2m, wind10m```
1. Notice that dataseries contains multiple forecast entries. Each timepoint indicates how many hours after the forecast was initialized the entry applies.

