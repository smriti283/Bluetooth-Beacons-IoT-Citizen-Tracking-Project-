# Internet-of-Things Privacy and Security: Citizen Tracking in Public Spaces

## Overview

Most businesses track consumers for user engagement and marketing purposes, yet don’t explicitly state so. While some forms of consumer tracking such as surveillance cameras and tracking cookies are widely known, many of us are unaware that companies use additional, obscure technologies and third party apps to track consumers in private and public spaces without their knowledge or full consent. This raises privacy concerns, since little is known about the extent of this data collection, such as the technologies utilized and the use of the data. 

This project focuses on investigating consumer tracking in public spaces through the use of one such covert technology - Bluetooth Beacons, that is now widely employed by location tracking companies, but remains largely unknown and undetectable to the general public. By gaining a firm understanding of the technology and using Android based apps for beacon detection, we aim to build a beacon location database for two retail-centric boroughs in New York City- Manhattan and Brooklyn; in order to draw insights on the participating companies and the third party vendors involved. With this work we intend to raise awareness regarding consumer tracking to eventually inform and push for reforms in data-sharing regulations and data privacy laws that ensure transparency, and ensure a legitimate purpose for the data collection processes. 

## Dataset

### Beacon Network Dataset:

Given the lack of a pre-existing database of beacon usage in the retail landscape of New York City, we have built a dataset for further analysis and geospatial mapping. To gain a holistic overview of beacon network in the city, we have followed a two-fold approach towards data collection:
- Beacon data + GPS locations data collection using two Android based apps simultaneously.
- Industry and company research for identification of beacon manufacturing companies and the unique identifiers in their products.

### Supporting Datasets/ APIs:

- NYC Census Tracts Shapefile (2020) : This dataset was retrieved from the website of NYC Department of City Planning and can be accessed at https://www1.nyc.gov/site/planning/data-maps/open-data/census-download-metadata.page . It represents the 2020 Census Tract boundaries from the US Census for New York City and are derived from the US Census Bureau's TIGER data products. For proper representation of geographical areas, the multipolygons in this dataset were exploded into simple polygons before geospatial plotting. 
- Google Maps API: Google Maps APIs is a set of 14 application programming interfaces owned by Google LLC that navigate people to interact with location-based Apps. These have been used for visualization of beacon signal locations.  
- Reverse Geocoding APIs: Reverse geocoding involves identifying address data by querying latitude and longitude coordinates. To convert GPS locations of beacon data to a readable/ identifiable address for a clearer picture of where they could be housed, Reverse Geocoding, using Nominatim by OpenStreetMap.org, has been applied to the dataset achieved after 30-second reduction.

## Methodology

1. Research on Technology and Manufacturing Companies
2. Data Collection Feasibility Checks and Testing
3. Large scale beacon data collection
4. Data processing 
5. Analysis and Visualizations

## Results

### 1. Research on Technology and Manufacturing Companies

#### Company Research

We began with conducting industry research to find beacon manufacturers and their product UUID formats. Our methods included internet research, media research, cold calls and product demos. We also leveraged internet searches of the UUIDs captured during our data collection process (step 2), to identify additional beacon manufacturing companies.

Through this study, we were able to identify 53 beacon manufacturing companies across the world, and were able to map UUIDs against 40 of these companies. This dataset is converted to a ‘.csv’ file for further use.

#### Technology Research

On the tech side, we conducted research on SDKs and app-libraries to understand the information flow ecosystem between retailer, beacon device, app and the user. Our primary technology research method was through the internet. 

Our research revealed that beacons do not engage in data collection or sharing by themselves. Beacons transmit signals to a bluetooth device to know your location details. Once this is received, they trigger and send your location data to the third-party apps embedded into common apps / retailer's app, which collects and shares information. 

### 2. Data Collection Feasibility Checks and Testing

While step 1 was in progress, we parallelly tested out several methods to ensure successful data capture, often undergoing several iterations to find solutions to the problems encountered. Before we could begin full-scale dataset building, we carried out a pilot data collection exercise in New York City.

We used the existing open-source Android based app called 'Beacon Scanner' by Nicolas Bridoux, which scans for nearby beacon signals and logs Beacon UUID, major, minor, user-proximity and timestamp. To test this, we walked around three neighborhoods in NYC with retail stores concentration to scan for beacon signals in public spaces. The geographic locations of scanning sites and times of scans were manually logged on an excel spreadsheet, along with stores in the vicinity. The data from the Beacon Scanner app is logged into a data-collection server in real time, which was built by our sponsor.

Through this exercise, in a total of 72 minutes of scanning, we were able to build a dataset of 6513 records. 80 unique UUIDs were captured across the dataset. Moreover, based on the timestamps in the dataset and location mapping chart of data collection, we were able to identify the potential retailers that house 9 such detected beacons. 

### 3. Large scale data collection

Logging GPS locations manually was not feasible for a full scale data collection exercise. So, to automate the process of GPS collection, we decided to use the 'GPS Logger' app by BasicAirData, which uses a combination of satellites to detect and log the latitude and longitude coordinates of the user with timestamp.

Next, the city’s geography and the retail hubs were charted on a physical map. Given the limited time-frame of the project, the data collection geography was limited to the retail-centric areas of Manhattan and Brooklyn only. 

Three team members were designated to collect data across the designated geographies, by walking on sidewalks and public spaces using both apps simultaneously for data collection.

In a total of 2555 minutes of data collection and using three Android phones, the team covered approx. 102 kms of distance within 129 census tract geographies across the two boroughs, and collected approximately 346,887 records of beacon signal hits.

### 4. Data Processing

The final dataset is achieved by pre-processing the data (such as flattening nested dictionaries etc.) and merging the beacon scanner data and GPS data on timestamp, giving us records of beacon signals with the approximate location coordinates based on the date and time of data collection. 

To account for duplicate records due to potential repeated scanning of the same beacon device, the beacon signals with the same set of UUID, major and minor that are detected within 30 seconds of initial detection are removed. After this reduction, we are left with a dataset consisting of 10,357 records of beacon counts.

The resulting dataset was then merged with census geometries and manufacturing company details. Time spent on each census tract was calculated and reverse Geocoding was applied on this merged dataset to obtain street level address information of each beacon.

### 5. Analysis and Visualizations

With the above dataset, we aim to present beacon activity in public spaces within Manhattan and Brooklyn. Therefore, the data is analyzed to check for insights such as number of unique UUIDs, top UUIDs detected, details on manufacturing companies, mapping of detected beacons, their physical addresses and potential retail stores identification etc. 

To communicate the findings, we used several tools to build effective visualizations. These can be accessed at the links given below: 

#### Beacon Activity Distribution

![
[Beacon Mapping using Google Maps JavaScript API](https://nbviewer.org/github/claugomzz/iot-capstone/blob/main/Visualization/IoT_Google%20API%20map.html)
[Geographical Distribution and Nos. of Beacons using D3.js, Plotly JS and Mapbox](https://mlab.engineering.nyu.edu/beacon/iot-capstone/Visualization/Final_Capstone.html)
[Census Tract level Beacon Distribution using Tableau Dashboard](https://public.tableau.com/app/profile/gexinliu/viz/CensusAgg/1_1?publish=yes)

