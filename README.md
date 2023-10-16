# Community Resources Mapping Platform For Disaster Preparedness

## Index

| Table of Contents  |
| ------------- | 
| [Introduction](#Introduction)  | 
| [Research Problem and Key Ideas to Address](#Research-Problem-and-Key-Ideas-to-Address)  | 
| [Data Collection Methodology and Its Structure](#Data-Collection-Methodology-and-Its-Structure)  | 
| [Dashboard Design Methodology](#Dashboard-Design-Methodology)  | 
| [Dashboard Installation and Key Functions](#Dashboard-Installation-and-Key-Functions) |
| [Benefits and Potential Improvements](#Benefits-and-Potential-Improvements)  | 

## Introduction
### Purpose and importance of the project
By enhancing the quality of data regarding local community capabilities, resources, and assets, the initiative aims to facilitate local community disaster preparedness and hence improve community resilience. It aspires to produce fresh approaches to community service and disaster preparedness at the local level.


### Current trends and challenges in the field
1. Choosing appropriate sources of information: How do we ensure the collected data is accurate and reliable?
2. Processing and analyzing resource data
3. Building data capability 

## Research Problem and Key Ideas to Address
### What is our concrete research problem to address?
Emergency preparedness and response continue to be hampered by a lack of data, inadequate data access, and low-quality community-level data, particularly in Australia's rural and regional areas that are prone to emergencies.
### What are our key ideas incorporated into our dashboard
The objectives of dashboard application is for providing a platform  
- where people can contribute to the collection of resources for bushfire recovery 
- where the general public can find the immediate support near their location during or after Fire Danger Period
- that can showcase the capability of community resources potentially available aftermath of a bushfire 
## Data Collection Methodology and Its Structure
### Overview of data collection flows
Initially, data collection was focused on three target locations, namely Ararat, Beechworth and Bright. Data was extracted from various sources including OpenStreetMap, Google Maps and PlaceName. Once the data was collected, they were processed and some data cleaning steps were performed such as filling missing values, and the data was merged. Once data was finalised, they were categorised as belonging to amenity, transport, road, people, and disaster types.  
A diagram demonstrates the steps taken in collecting and preprocessing the dataset

[Click me for link to the Pipeline of Data Gathering:](https://app.diagrams.net/?src=about#Wb!F4mXYAbAxk65hP34TSrX_G_JJ8NjuWlBvpkagtBqF5X4VQfv52MJSbsAzRyR2ona%2F016YO6OILT7WA6YHNLHJF3MUPXGL4OUGS2)
![pipeline_data gathering V2](https://user-images.githubusercontent.com/77183391/235133589-f8e88b0d-3336-4678-9be2-9ef6d00b9d2b.jpg)

### The 5 type of data
amenity, transport, road, people, disaster types
### Three layer data structure
Each layer consists of a number of categories: For example, the amenity have categories of Health, Emergency, Care, Education etc. Disaster types could be catgorised by Flood and Bushfire prone area
Each category consists of a number of features: For example, the Emergency category is comprised of police station and fire station 
Each feature has a number of entities
Each entity has its own a set of attributes: phone number, locations, website, attributes 

### Present the details of the attributes of each entity
**AMENITY**<br />

[Link to dataset:](https://github.com/pccxxxy/bushfire_preparedness_data_mapping/blob/main/Data%20Gathering/final/amenity.xlsx)


*Data type of the final data:* xlsx
Data Structure:
| Purpose | Column name | Notes |
| --- | --- | --- |
| Item naming | - Name: the name of the amenity||
| Classification |- Feature<br /> - Category| No public university and institutions found in Ararat, Beechworth and Bright. |
| Location |- Latitude: The measurement of distance north or south of the Equator<br /> - Longitude: The measurement of location east or west of the Equator- Address:address of the amenity| |
| Contact |- Website: website of the amenity<br /> - Phone: phone number of the amenity<br /> - Email: Email address of the amenity| Amenities under 'utility' category such as patrol station, charging station and toilets don't have a website, phone and email. Small-scaled Amenities don't have website, phone or email.If any amenity doesn't have a phone number but has other contact details published, we pull the email as an alternative. If the amenity doesn't have a website, we use its social media page or other relevant website having the amenity's information on it. |
| Other information |- Attributes:- Mental support: free or paid services to support mental health<br /> - Living essentials: Food, Water, Clothes, laundry services, internet, charging ports<br /> - Emergency tools: First aid kits, Fire extinguisher, water tank, dam or pool, Fire Blankets, Fire Hose Reels, sprinklers<br /> - Financial assistance: financial recovery program, financial recovery product, funding support<br /> - Accessibility support: any facilities or services for people with disabilities<br /> - Shelter: free accommodation, church, specific paid accommodation with relevant facilities||
| Working purpose |- Relevance: indicate the relevance of item<br /> - Source\_placename: indicate whether the data of item is sourced from Placename<br /> - Source\_google\_map: indicate whether the data of item is sourced from Google Map<br /> - Source\_osm: indicate whether the data of item is sourced from Open Street Map| Kinders, schools and educational centers are classified as irrelevant because in case of a bushfire this might be shut down. The same item may be available from multiple data sources, and so a few items have multiple source columns filled in. Source columns are serving for working purposes only and will be excluded in the dashboard building.|
### Sources where the data is collected

- Open Street Map (all categories | columns covered: title, features, latitude, longitude, attributes, address)
- Google map (all categories | columns covered: title, feature, latitude, longitude, address, website, phone, email, attributes).
- Place name (all categories | columns covered: title, feature, category, latitude, longitude, address, website, phone)

### Steps taken to get the final data

1. Query the Open Street Map data in target location using QGIS
2. Manually filter out the Open Street Map data that is out of focus
3. add missing coordinates to Open Street Map data using QGIS
4. Query Google Map data using Phantombuster
5. Download Placename data from Placename web portal
6. rganize Placename data into a structured spreadsheet by delimiter
7. merge data from all data sources into one spreadsheet for each target location, using Python
8. merge repeating rows into one row manually or using Excel function
9. fill in the missing address using reverse-geocoding in Python
10. Drop the data outside target location using Python
11. Fill in the essential information including website, phone, emails) using manual Google search
12. Fill in the additional information including attributes using manual Google search
13. Add column indicating the source and relevance of data
14. Removed duplicated items, fix erotic rows such as wrong address, missing coordinates and outdated information


**TRANSPORT**<br />

[Link to dataset:](https://github.com/pccxxxy/bushfire_preparedness_data_mapping/blob/main/Data%20Gathering/final/transport.xlsx)<br/>
*Data type of the final data:* xlsx
Data Structure:
| Purpose | Column name |
| --- | --- |
| Item naming |- Name|
| Classification | - Category: </br> <ul><li>public: public provider of transportation</li><li>Private: private provider of transportation</li></ul> - Feature: <ul><li>Bicycle hire</li><li>Bus operator</li><li>Bus stop</li><li>Taxi</li><li>Train station</li><li>Vehicle hire</li></ul> |
| Location |- Latitude: The measurement of distance north or south of the Equator<br/>- Longitude: The measurement of location east or west of the Equator|
| Contact information | - Phone<br/> - Email<br/> - website<br/> - Address |
| Source |- source\_ travelvictoria: column to indicate the data of item is sourced from Open Street Map<br/>- source\_gmap: column to indicate the data of item is sourced from Google Map|

### Sources where the data is collected

- [https://www.travelvictoria.com.au](https://www.travelvictoria.com.au/) (Private bus operators, taxis)
- google map (Private bus operators, public bus stops, train stations)

### Steps taken to get the final data

1. Obtain the dataset from the Travelvictoria website manually
2. Get the additional dataset from Google map through manual search
3. Merge dataset from all sources together into one spreadsheet per location
4. Corrected those mistakenly classified as 'bus stop' category to 'private bus operator' category
5. Added columns indicating the source of data


**ROAD**<br />
[Link to Ararat dataset](https://github.com/pccxxxy/bushfire_preparedness_data_mapping/blob/main/Data%20Gathering/final/highway_ararat_restructured.xlsx)
[Link to Bright dataset](https://github.com/pccxxxy/bushfire_preparedness_data_mapping/blob/main/Data%20Gathering/final/highway_beechworth_restructured.xlsx)
[Link to Beechworth dataset](https://github.com/pccxxxy/bushfire_preparedness_data_mapping/blob/main/Data%20Gathering/final/highway_bright_restructured.xlsx)
*Data type of the final data:* xlsx
Data Structure:
| Purpose | Column name | Notes |
| --- | --- | --- |
| Item naming |- Name |
| Classification | - Category: highway<br/> - Feature: <ul><li>Cycleway</li><li>Footway</li><li>Path</li><li>Primary</li><li>Primary\_link</li><li>Proposed</li><li>Residential</li><li>Secondary</li><li>Service</li><li>Tertiary</li><li>Track</li><li>Unclassified</li></ul> | Apparently, all data in the ‘Category’ of road data are highway. 
| Location |- Latitude<br/>- Longitude<br/>- Length<br/>- Straightdis<br/>- Sinuosity||
| Other information | - wheelchair: places or ways that are suitable to be used with a wheelchair and a person with a disability who uses another mobility device (like a walker).<br/>- footway: minor pathways which are used mainly or exclusively by pedestrians.<br/>- motor\_vehicle: This property is used for all types of roads but not for gates<br/>- tracktype: A measure of how well-maintained a track or other road is, particularly regarding surface firmness.<br/>- width: The key **width** describes the _actual_ width of a way or other feature.<br/>- foot: Whether the route can be used by pedestrians.<br/>- lanes: individual lanes of a road.<br/>- bicycle: Legal restriction for cyclists.<br/>lit: indicates the presence of lighting.<br/>- surface: The **surface** key is used to provide additional information about the physical surface of roads/footpaths and some other features, particularly regarding material composition and/or structure.<br/>- maxspeed: define the maximum legal [speed limit](https://wiki.openstreetmap.org/wiki/Speed_limits) for general traffic on a particular road, railway or waterway.<br/>- oneway: indicate the access restriction on [highways](https://wiki.openstreetmap.org/wiki/Highway) and other linear features for vehicles as appropriate.<br/>- carriageway: whether the road has single or dual carriageway. <br/>- name: any kind of road, street or path <br/>- mtb:scale:uphill :This is used for classifying the level of difficulty of using a [way](https://wiki.openstreetmap.org/wiki/Way) that is more or less level (no inclination) or is used for riding down.<br/>- mtb:scale:imba :A classification scheme for the difficulty of specifically designed trails for mountainbiking.<br/>- smoothness : provides a classification scheme regarding the physical usability of a way for wheeled vehicles, particularly regarding surface regularity/flatness.||
| Highway colums | - route: route for highway. The name of routes such as A8, C148 and B180 can tell if the highway is a dual or single carriage way.<br/>- from: origin <br/>- via<br/>- to:destination| Ararat, Beechworth and Bright don't have highway routes in M type. M type are dual carriageways with at least two lanes in each direction. Therefore, there is no dual carriageway for the major highways in target location|


### Sources where the data is collected

- OSM(all categories)
- [https://en.wikipedia.org/wiki/List\_of\_highways\_in\_Victoria](https://en.wikipedia.org/wiki/List_of_highways_in_Victoria)(Highway, Route type of highway)
- [https://www.travelvictoria.com.au/victoria/roads/](https://www.travelvictoria.com.au/victoria/roads/)(Route type of highway)

### Steps taken to get the final data

1. Query dataset from Open Street Map using QGIS
2. Obtain the additional dataset from Wikipedia
3. Compare Open Street Map dataset with the Wiki data and information on TravelVictoria
4. For the duplicated items in Wiki, merge them with OSM data into one row and fill the missing values in 'road' and 'route' columns using Wiki data
5. For the unseen items in Wiki and if they pass target locations, add them as a new row and fill the missing values in 'road' and 'route' columns using Wiki data
6. Add 'from', 'via', 'to' and 'carriageway' as new columns
7. Add 'longitude' and 'latitude' for the Wiki data by searching for highway locations using Google Map GPS feature

**PEOPLE**<br />

[Link to dataset:](https://github.com/pccxxxy/bushfire_preparedness_data_mapping/blob/main/Data%20Gathering/final/people.xlsx)
*Data type of the final data:* xlsx
Data Structure:

| Column name | Description |
| --- | --- |
| category |- Whether it is a Registered nonprofit organisation, Non-profit groups created by individuals, or authorized organization.|
| name |- People data name|
| Feature |- To select from features under each category.|
| Volunteer |- Whether there are volunteers|
| Attribute |- Gives more information about the particular data.|
| Followers |- Indicating how popular the page is if it is a social media page.|
| Location |- Latitude: The measurement of distance north or south of the Equator- Longitude: The measurement of location east or west of the Equator|
| Contact information | phonewebsiteaddress |
| Source |- Source\_Community\_Directory: Data obtained from community directory- Source\_Social\_Media: Data obtained from social media- Source\_Amenity: Data obtained from previously collected amenity data|


### Sources where the data is collected

- Facebook, Twitter, links suggested by existing bushfire apps, My Community Directory (Non-profit groups created by individuals, Volunteer)
- Selectively reuse those data we've already got for amenity data including rows featured with Neighbourhood Safer Place, Church, SES facility, Non-profit organization, Thrift store, Local government office, State government office, Community center and Local government office (Registered Non-profit organisation, authorized organization)

### Steps taken to get the final data

1. Find any existing platfoms, case studies, webpages and social media channels that publish people resources available in local communities during the bushfire season
2. Select those relevant and can cater for Ararart, Beechworth and Bright.
3. Organize the data selected to spreadsheet
4. Find those non-profit origanizations having people resources available from the amenity data
5. Re-organize the data in spreadsheet, while the data above being added


**PAST BUSHFIRE**<br />
[Link to dataset:](https://github.com/pccxxxy/bushfire_preparedness_data_mapping/blob/main/Data%20Gathering/final/bushfire_targetlocations.xlsx)
*Data type of the final data:* xlsx
Data Structure:


| Column name | Description |
| --- | --- |
| category |- The type of disaster|
| brightness |- Brightness of Bushfire|
| scan ||
| track ||
| acq\_date ||
| acq\_time ||
| satellite ||
| instrument ||
| confidence ||
| version ||
| bright\_t31 ||
| frp ||
| daynight ||
| Place ||
| Type ||



**BUSHFIRE PRONE AREA**<br />
[Link to dataset:](https://github.com/pccxxxy/bushfire_preparedness_data_mapping/blob/main/Data%20Gathering/final/bushfire_risk.csv)
*Data type of the final data:* xlsx
Data Structure:


| Column name | Description |
| --- | --- |
| LGA\_CODE ||
| LGA\_NAME ||
| PLAN\_NO ||
| GAZETTAL ||
| BPA\_AREAHA ||
| geometry ||
| BUSHFIRE\_RISK\_LEVEL ||
| category ||

### Steps taken to get the final data

- Combine Bushfire\_prone\_area.shp representing the LGA boundary of bushfire prone area, together ath the bushfire\_risk.csv indicating the risk level based on common LGA name


**LGA BOUNDARY**<br />
[Link to Ararat dataset](https://github.com/pccxxxy/bushfire_preparedness_data_mapping/blob/main/Data%20Gathering/final/coordinates%20on%20boundary_ararat.xlsx)

[Link to Bright dataset](https://github.com/pccxxxy/bushfire_preparedness_data_mapping/blob/main/Data%20Gathering/final/coordinates%20on%20boundary_beechworth.xlsx)

[Link to Beechworth dataset](https://github.com/pccxxxy/bushfire_preparedness_data_mapping/blob/main/Data%20Gathering/final/coordinates%20on%20boundary_bright.xlsx)

*Data type of the final data:* xlsx
Data Structure:
| Column name | Description |
| --- | --- |
| Latitude | list of latitude helped forming the boundary of each region |
| Longitude | list of longitude helped forming the boundary of each region|
| Place | Name of target location |

### Steps taken to get the final data

1. Search for the region of Ararat, Beechworth, Bright from OSM search in QGIS
2. Once these regions being mapped on QGIS as layers, convert each of these layers from polygon data to point data (list of coordinates forming the boundary of each region)
3. Highlight all the points data
4. Export the point data of each layer into a separate csv file.






## Dashboard Design Methodology

### Design paradigm and approach
A wireframe showcases the layout of dashboard and its functions

[Click me for link to the Dashboard design:](https://lucid.app/lucidchart/da7b6046-82fc-4be6-9190-a7fffe90f47b/edit?viewport_loc=-95%2C31%2C2299%2C1278%2CmY0PIeC.0Trf&invitationId=inv_41ae1e99-4673-4d0d-bc2a-980e6efb2cb8)
![Dashboard design](https://user-images.githubusercontent.com/77183391/235130663-0358d792-478f-4184-ada1-f84741ee7798.png)


### Dashboard Software Architecture
A flowchart explains how the different functions work with each other within dashboard in the program's perspective

[Click me for link to the Dashboard software architecture:](https://lucid.app/lucidchart/99e5746c-ec90-437f-aa93-7aa993da8db8/edit?invitationId=inv_c4cd7f69-7220-44bb-9c37-ceb2e55c83c4)
![architecture diagram](https://user-images.githubusercontent.com/77183391/235131296-84837f5b-8f2d-4b1c-a11c-723fc7e4f7ee.png)


### Workflow of Dashboard
A flowchart instructs how to to use the dashboard with the employed functions in in the user's perspective
<img width="632" alt="Screenshot 2023-04-28 at 9 06 23 pm" src="https://user-images.githubusercontent.com/77183391/235132065-8f1bb3b4-406e-4771-932e-303cf26252d0.png">

## Dashboard Installation and Key Functions
### Installation guideline
#### Prerequisite

Make sure packages in this section are installed prior to running the application.

Packages can be installed on your local computer or any of those virtual environments below:

- Pipenv
- Poetry
- Venv
- Virtualenv
- conda

**Python**

**PIP**

[**Folium (Version 0.14.0)**](https://python-visualization.github.io/folium/)


Folium is a python library used for visualizing geospatial data. This library was installed using the pip command.

_pip install folium_

[**Streamlit (Version 1.19.0)**](https://streamlit.io/)

Streamlit is an open-source app framework used to build web applications.

This library was installed using the pip command.

_pip install Streamlit_

[**Streamlit-folium (Version 0.11.1)**](https://folium.streamlit.app/)

_pip install streamlit-folium_

[**streamlit-tree-select (Version 0.0.5)**](https://discuss.streamlit.io/t/new-component-streamlit-tree-select-a-simple-and-elegant-checkbox-tree/30195)

_pip install streamlit-tree-select_

**Other Python libraries used:**

pandas

seaborn

geopandas
### How to use
1. Open terminal in your IDE or Python terminal
2. Type 'streamlit run streamlit\_app.py' to start Streamlit server
3. To stop the Streamlit server: Ctrl+c

Initial view of the dashboard. The user can first enter the target location in the search bar.
<img width="1440" alt="MicrosoftTeams-image (3)" src="https://user-images.githubusercontent.com/60376904/236654660-114e4620-a052-4f4f-b380-0c0042e83e57.png">

After entering the target location, user can select checkboxes on the left based on required resources. Once selected, the data can be downloaded as a csv file as well. The selected amenities and their features will be displayed on the right.
<img width="1440" alt="MicrosoftTeams-image (4)" src="https://user-images.githubusercontent.com/60376904/236654771-24589df1-b410-47bd-b5e6-7e234790254f.png">
<img width="1440" alt="MicrosoftTeams-image (5)" src="https://user-images.githubusercontent.com/60376904/236654838-1ab4b101-18b7-4127-8e27-070ce5de978d.png">

User can also opt to upload their own csv files which will then be displayed on the map.
<img width="1440" alt="MicrosoftTeams-image (6)" src="https://user-images.githubusercontent.com/60376904/236654851-8329fe64-78ae-41dd-b01b-56829550f56e.png">






### Key technical components
#### Key files in Dashboard code pack

[**Streamlit\_app.py**](https://github.com/pccxxxy/bushfire_preparedness_data_mapping/blob/main/src/dashboard/streamlit_app.py)

The code of Dashboard application

[**/data**](https://github.com/pccxxxy/bushfire_preparedness_data_mapping/tree/main/src/dashboard/data)

All dataset used in this application

[**/experiment**](https://github.com/pccxxxy/bushfire_preparedness_data_mapping/tree/main/src/experiment)

Codes used for debugging and testing of particular functions throughout the development

[**/preprocess**](https://github.com/pccxxxy/bushfire_preparedness_data_mapping/tree/main/src/preprocess)

Codes used for preprocessing the dataset before developing the application

[**Requirement.txt**](https://github.com/pccxxxy/bushfire_preparedness_data_mapping/blob/main/src/dashboard/requirements.txt)


## Benefits and Potential Improvements
### What are something to be further improved?
1. It would be good to include live data available from geographic areas. A possible way to do this can be by using live cameras.
2. Communities would already have localised practices in response to disasters. We can try to incorporate this into the dashboard.
3. Only allow permitted users to upload data.
4. Save the data uploaded to our database.
### What are expected benefits from the outcomes of this project
The  outcome of the project, which is an open platform dashboard achieved the digitalisation of the crisis recovery. 

The components built in dashboard prepares people to be ready for upcoming disaster at anywhere anytime, by offering them with contacts, exact locations having streetviews where available, and potential attributes of local resources in regional Victoria that's likely to come to be available in bushfire seasons and useful before, during or after a bushfire. 

Taking the benefits of data mapping techniques, the dashboard showcases the capability of those existing data gathered. The mapping of local knowledge, for example, intuitively take people to one or more features/categories of infrastructure nearby on a map that they are looking for. Mapping on a selection of people resources is the best illustration of humanitarian mapping that are up-to-date, localised and reachable, telling information about group of people who can offer supports case by case during Busfire seasons. Data mapping of Bushfire Prone Area, complements the focus on mapping risks and impact zones of bushfire prone areas across Victoria. 

Additional functions such as Data Donation and Data Export, generate new ways of volunteering and acting locally toward diaster preparedness, but also reveal the potentiality of updating the existing database on Live in the future production of this project. 


# Appendix A: Useful Online Links, Blogs, and Information about Bushfire and Emergency Preparedness

## 1. Factors Influencing Bushfire Behaviour
- [CSIRO - Bushfires 2019-20 Explainer](https://www.csiro.au/en/research/natural-disasters/bushfires/2019-20-bushfires-explainer)

## 2. Bushfire Information for Victoria
- [Royal Commission - Chapter 9: Community Safety](https://naturaldisaster.royalcommission.gov.au/publications/html-report/chapter-09)
- [Indigo Shire Council - Prepare for an Emergency](https://www.indigoshire.vic.gov.au/Residents/Emergencies/Prepare-for-an-emergency)
- [Fire Rescue Victoria - Specialist Response](https://www.frv.vic.gov.au/specialist-response)

## 3. Data Sources (Ararat, Beechworth, Bright)
- [Planned burns last 10 years](https://www.emergency.vic.gov.au/prepare/#fire/planned-burns-last-10-years)
- **Bushfire Information**:
  - [Real-time fire alert](https://www.abc.net.au/emergency/warning/4556fd22-968d-11ec-8dc7-0a854d6001e6)
  - [Current fire danger rating](https://www.emergency.vic.gov.au/prepare/#fire/fire-danger-ratings)
  - [Real-time Fire severity](https://hotspots.dea.ga.gov.au/#/)
  - [Heat, wind, fire, and impact areas alert](https://www.emergency.vic.gov.au/respond/#)
- **Temperature Information**:
  - [Bureau of Meteorology - Fire Weather Warnings](http://www.bom.gov.au/metadata/catalogue/19115/ANZCW0503900440?template=full#distribution-information)
  - [Latest Weather Observations for Victoria (Ararat)](http://www.bom.gov.au/vic/observations/vicall.shtml)
- **Wind Information**:
  - [Real-time wind moving pattern across Vic](http://www.bom.gov.au/watl/wind/forecast.shtml?unit=p0&location=vic&tz=AEDT#terms-of-use)
- **Humidity Information**:
  - [Relative Humidity Averages](http://www.bom.gov.au/jsp/ncc/climate_averages/relative-humidity/index.jsp)

## 4. During Bushfire: Unblock Obstacles in Evacuating & Rescuing People
- **Identify Telecommunications Constraint**:
  - [Real-time Power outage alert](https://www.powercor.com.au/power-outages-and-faults/full-outage-list/)
- **Identify Traffic Constraint**:
  - [Current regional roads in maintenance](https://regionalroads.vic.gov.au/map#?name=Beechworth&east=146.7619779332695&north=-36.24622401099226&south=-36.42160917495426&west=146.5579661727982&project=2c663fe33b454f4fa395514d92c2779e)
  - [Traffic incidents and alerts](https://traffic.vicroads.vic.gov.au/incidents/4974977)
- **Enable EST Operators to Provide Directional Information**:
  - [Emergency service telecommunications authority Emergency Markers by road type (Ararat)](https://nationalmap.gov.au/#share=s-AhxQd3fuoYgHyqpkoXJxLcAOyry)
  - [ESTA Emergency marker full (Ararat)](https://data.gov.au/dataset/ds-dga-77ec8fb6-ccee-4937-a266-9706899d78f9/details)
- **Identify How Many/What Emergency Facilities Cover Your Location**:
  - [Emergency Relief Provider Counts](https://nationalmap.gov.au/#share=s-AhxQd3fuoYgHyqpkoXJxLcAOyry)
  - [Emergency Relief Provider Outlets](https://nationalmap.gov.au/#share=s-tdQz19jJn5EGWy05yIt4Y3bcjAS)
  - [Emergency management facilities](https://nationalmap.gov.au/#share=s-s5KmhqBW3Jjyp0nQfhLIgxtfpSt)
  - [Fire Rescue Vic Response area Map](https://www.frv.vic.gov.au/response-area)
  - [Areas covered by CFA & MFB](https://www.emergency.vic.gov.au/prepare/#fire/risk/cfa-mfb-district-boundaries)
- **Map Out the Closest Safe Place Near Me**:
  - [Low bushfire rating area](https://discover.data.vic.gov.au/dataset/low-bushfire-rating-areas1)
  - [Safe places in all locations](https://www.emergency.vic.gov.au/prepare/#fire/risk/neighbourhood-safer-places)

## 5. After Bushfire: Identify Relief Resources Available After the Bushfire
- [First Aid Directory](https://shorturl.at/jnF03)
- [Crisis & Emergency Accommodation](https://shorturl.at/ozDFG)
- [Bushfire assistance provider](https://rb.gy/u3crq)

## 6. Other Datasets
- **Bushfire Data for Victoria and Australia**:
  - [Victorian bushfire data](https://rb.gy/hae5u)
  - [Australia health sites](https://data.humdata.org/dataset/australia-healthsites)
  - [Our airports Australia](https://data.humdata.org/dataset/ourairports-aus)
  - [Neighbourhood Safer Places in Victoria](https://www.cfa.vic.gov.au/plan-prepare/your-local-area-info-and-advice/neighbourhood-safer-places)
  - [Public hospitals in Victoria](https://www.health.vic.gov.au/hospitals-and-health-services/public-hospitals-in-victoria)
  - [Royal Commission Natural Disaster Report (Chapter 12)](https://naturaldisaster.royalcommission.gov.au/publications/html-report/chapter-12)
- **Global Bushfire Data**:
  - [NASA MODIS Program](https://modis.gsfc.nasa.gov/data/): The global bushfire data was obtained from the NASA Moderate Resolution Imaging Spectroradiometer (MODIS) program. This website provides access to a wide range of satellite data, including information

- **Bushfire Prone Areas in Victoria, Australia**:
  - [Victoria State Government](https://datashare.maps.vic.gov.au/): The information about bushfire-prone areas in Victoria, Australia, was sourced from the official website of the Victoria State Government. This website provides detailed maps and data related to bushfire-prone regions within Victoria, facilitating the understanding and assessment of areas at risk of bushfire incidents.

## 7. Regional Data

### ARARAT
- **Food Relief**:
  - [Ararat Neighbourhood House](https://www.araratneighbourhoodhouse.com.au/anh-food-hub/)
  - [Health Direct - Food Relief in Ararat](https://www.healthdirect.gov.au/australian-health-services/results/ararat-3377/tihcs-aht-23106/food-relief?pageIndex=1&tab=SITE_VISIT)
- [Neighbourhood Safer Places in Ararat](https://www.ararat.vic.gov.au/services/emergency/neighbourhood-safer-places)
- [Disability Services in Ararat](https://www.disabilitysupportguide.com.au/search/24-hour-emergency/ararat-vic)

### Alpine (Bright)
- [Alpine Shire Council - Fire, Flood, and Emergencies](https://www.alpineshire.vic.gov.au/council/fire-flood-and-emergencies)
- [Alpine Preparedness Newsletter 2021](https://www.alpineshire.vic.gov.au/sites/default/files/Alpine%20Preparedness%20Newsletter%202021.pdf)
- **Food Relief**:
  - [Health Direct - Food Relief in Bright](https://www.healthdirect.gov.au/australian-health-services/results/bright-3741/tihcs-aht-23106/food-relief?pageIndex=1&tab=SITE_VISIT)
- [Disability Services in Bright](https://www.disabilitysupportguide.com.au/search/location/bright-vic)
- [Alpine Shire Municipal Emergency Management Plan 2021-2024](https://www.alpineshire.vic.gov.au/sites/default/files/resources/Alpine-Shire-Municipal-Emergency-Management-Plan-2021-2024_0.pdf)

### Indigo Shire (Beechworth)
- [Emergency Relief Centres in Indigo Shire](https://www.indigoshire.vic.gov.au/Residents/Emergencies/Emergency-Relief-Centres)
- [Disability Services in Beechworth](https://www.disabilitysupportguide.com.au/search/location/beechworth-vic)
- [Municipal Emergency Management Plan 2022 (Redacted)](file:///C:/Users/Admin/Downloads/Municipal-Emergency-Management-Plan-2022-Redacted.pdf) *(Note: This is a local file link and won't work for others accessing the README on GitHub)*

### Yarra Ranges Council
- [Community Transport in Yarra Ranges](https://www.yarraranges.vic.gov.au/Community/Health-and-Wellbeing/Community-relief-and-support-agencies/Community-transport)
- [Food Relief in Yarra Ranges](https://www.yarraranges.vic.gov.au/Community/Health-and-Wellbeing/Community-relief-and-support-agencies/Food-relief-food-boxes-and-meals)
- [Disability Support Services in Yarra Ranges](https://www.yarraranges.vic.gov.au/Community/Health-and-Wellbeing/Community-relief-and-support-agencies/Disability-support-services)
- [Community Health Services in Yarra Ranges](https://www.yarraranges.vic.gov.au/Community/Health-and-Wellbeing/Community-relief-and-support-agencies/Community-health-services)

# Research Project Contributors

The following members of this research project are attributed due credit for their contributions:

* Prof. Anthony McCosker, Swinburne, ADM+S
* Dr Yong-Bin Kang, Swinburne, ADM+S
* Prof. Kath Albury, Swinburne, ADM+S
* Dr Frances Shaw, Swinburne, ADM+S
* Cindy Tao, Junior Business Intelligence Tester, Insurance Commission of Western Australia & Swinburne Alumni
* Sheba Ann Roy, Data Scientist - PBA Transit Planning Pty Ltd & Swinburne Alumni
* Cobi Calix, Research Fellow, Australian National University
