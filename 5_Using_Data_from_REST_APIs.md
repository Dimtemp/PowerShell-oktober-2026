# 5 Using Data from REST APIs

Many modern applications provide data via REST APIs. You will learn:
- How to call APIs using Invoke-RestMethod.
- Processing JSON data and converting it into usable objects.

## Note! In this exercise we rely on external APIs and information sources. There is no guarantee that these services are currently available, or work as expected.

# Representational state transfer (REST)
Representational state transfer (REST) is a software architectural style that defines a set of constraints to be used for creating Web services. Web services that conform to the REST architectural style, called RESTful Web services, provide interoperability between computer systems on the internet. RESTful Web services allow the requesting systems to access and manipulate textual representations of Web resources by using a uniform and predefined set of stateless operations. 


## Task: IP Info
1. Enter this command to store a URL in a variable: ```$url = 'https://ipinfo.io/json'```
1. Please notice that the URL is making a reference to json. The reply might contain JSON-formatted data.
1. Enter this command to retrieve the contents behind the URL: ```Invoke-WebRequest $url```
1. Notice the content property. This holds information for the network connection you are using to access the internet.
1. Inspect the output. Now store the output in a variable: ```$r = Invoke-WebRequest $url```
1. Inspect the variable: ```$r```
1. Inspect the content property: ```$r.content```
1. You can convert the textual output from JSON using this command: ```$r.content | ConvertFrom-Json```


## Task: Spot the International Space Station (ISS)
1. Enter this command to store a URL in a variable: ```$url = 'https://api.wheretheiss.at/v1/satellites/25544'```
1. Since the service offers data in JSON, we can use the Invoke-RestMethod command to retrieve data: ```Invoke-RestMethod $url```
1. Notice the visibility property. Eclipsed means you cannot see the ISS at this moment. If it displays 'daylight' it means you might be able to see it, but it will be very faint.
1. Select the relevant information: ```$r | Select-Object latitude, longitude, altitude, velocity, visibility```
1. You can optionally visit the corresponding website to visualize the location of the ISS. This should correspond to the visibility property from the previous command: ```https://wheretheiss.at/```


## Task: Explore a weather forecast
1. Store the URL for a forecast near Amsterdam in a variable: ```$url = 'http://www.7timer.info/bin/api.pl?lon=4&lat=52&product=civil&output=json'```
1. Retrieve the JSON response and store it in variable r: ```$r = Invoke-RestMethod $url```
1. Inspect the response: ```$r```
1. The forecast entries are in the dataseries property. Inspect the first entry: ```$r.dataseries```
1. Notice that dataseries contains multiple forecast entries. Each timepoint indicates how many hours after the forecast was initialized the entry applies. Also notice the output is a list, not a table.
1. Format the output as a table: ```$r.dataseries | Format-Table```
1. Display the forecast time, weather condition, temperature, and wind: ```$r.dataseries | Select-Object timepoint, weather, temp2m, wind10m```
1. Since we only select 4 properties, PowerShell defaults to a table.
1. Write it to an HTML file: ```$r.dataseries | Select-Object timepoint, weather, temp2m, wind10m | Convertto-html | out-file weather.html```
1. View the HTML file using this command: ```Invoke-Item weather.html```
1. A web browser opens the html file. Inspect the contents and close the tab.

# If time permits

## Task: Explore cascading stylesheets
1. Store a cascading stylesheet in a new variable: ```$css = '<style> th { background: darkblue; color: white; padding: 12px; } td { padding: 12px; } </style>'```
1. Use the new stylesheet and write it to an HTML file: ```$r.dataseries | Select-Object timepoint, weather, temp2m, wind10m | Convertto-html -Head $css | out-file weather.html```
1. View the HTML file using this command: ```Invoke-Item weather.html```
1. A web browser opens the html file. Inspect the contents and close the tab.
1. Store a slightly changed cascading stylesheet in a new variable: ```$css = '<style> th { background: red; color: white; padding: 12px; } td { padding: 12px; } </style>'```
1. Use the new stylesheet and write it to an HTML file: ```$r.dataseries | Select-Object timepoint, weather, temp2m, wind10m | Convertto-html -Head $css | out-file weather.html```
1. View the HTML file using this command: ```Invoke-Item weather.html```
1. A web browser opens the html file. Inspect the contents and close the tab.

