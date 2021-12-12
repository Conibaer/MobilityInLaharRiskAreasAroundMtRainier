## Mt. Rainier, 2020
![20200724_184443 copy](https://user-images.githubusercontent.com/91756808/145699807-ab020390-e51a-4e67-8689-e4f0a378d09d.jpg)
Photo taken by me, Chase B Barrows

## Mt. St. Helens, 2020
![20200724_190602 copy](https://user-images.githubusercontent.com/91756808/145699818-273854bf-3cd9-4eca-b815-84251dc00297.jpg)
Mt. St. Helens 2020
Photo taken by me, Chase B Barrows



# Lahar Risk around Mt. Rainier
This map shows the risk plane if a lahar event were to occur emanating from Mt.Rainier. Specifically, the risk zone resulting from a ‘case 1’ event. Defined by Hoblit et al(1998), case 1 events have occurred on 500 to 1000 year intervals for the last 5600 years and represent common but extreme Rainier lahar events with the yearly probability of occurrence between .1 and .2 percent. While an eruption event like that of Mt. St. Helens in 1980 by Rainier would most definitely result in a large lahar flow through its lower valleys and drainages. However geological research since the 1980s has shown that not all lahars from Rainier are directly linked to large eruption events. During the months leading up to the St.Helens eruption massive areas were evacuated for safety.  An eruption pattern like that of St.Helens by Mt. Rainier would no doubt be an extremely devastating event, but nonetheless would allow for vast warning time for the communities in the path of the mountain's destructive lahars. 

 Geochemical degradation of Mt. Rainiers rock structure by subsurface acidity from percolating and venting chemicals like sulfuric acid from far below the earth's crust have been shown to alter solid and structurally strong rock material into a weak-clay like consistency. This sticky, soft, red material is a noticeable feature of the summit rim as it sticks to climbers' crampons and gear.  As supported by geological evidence in today's lower Rainier drainages, the evidence suggests that Mt.Rainier is prone not only to eruption based lahars but also random earthquake triggered events or random and seemingly unprompted collapses. Even without the heat of eruption the mechanical movement of a massive collapse liquifies glaciers in a matter of seconds. With an estimated 156.3 billion cubic feet of ice(1986) even a small area of melt could cause a huge issue. Melt water mixes with geological material and becomes a muddy slurry that devastates any forest, animal, or human community in its way.
    
Many communities in the shadow of Mt.Rainier understand the risk of the geography they inahite and have set up early warning systems in case of a sudden collapse event. The town of Orting has city wide sirens and evacuation plans to high ground. With early warning sensors on Mt.Rainier's flanks they have about 30 minutes to evacuate in case of a sudden collapse event. That being said, certain areas within the lahar zones are prone to evacuation issues and increased risk. Availability of physical transportation infrastructure or accessibility, topography, and proximity to the mountain all play roles in evacuation dangers.

# What the Application does
The map application I’ve built is designed to help any user explore transportation needs and abilities within the  risk area for Rainier lahars. My application shows the lahar risk areas emanating from Mt.Rainier determined by the United States Geological Survey, updated 1998. Also included are Washington State public schools, K-12, that are within the lahar risk area. These are just one of many locations that deserve special evacuation consideration but are an obvious starting point for the user. By hovering over the schools the user can see the name of each school for reference. By clicking on the map in any location an isochrone polygon is created based on inputs from the upper left hand sidebar. By noting if the isochrone area extends beyond the lahar risk area the user can develop an idea of travel times in different modes of transportation in order to reach safety from any location. The schools provide a nice starting point to select as they are a high risk population with special considerations. A significant portion of the population are dependent on the emergency response of the state for transportation in case of emergency, but clicking anywhere on the map is also highly encouraged.

The town of Orting is a great example to inspect travel times. The town sits in a valley and is surrounded by steep topography. This topography limits transportation infrastructure up and out of the valley and into safer elevations. Many roads in and out of Orting simply follow the valley floor and do not offer a route to safety in the case of lahar flows. Clicking on one of the schools near the town center and changing the transportation settings to walking exemplifies the special risk the geography of the mountain imposes on Orting. Even with 30 minutes, one would have trouble exiting the low plane of the valley on foot. Not to mention the hurdles that are added by the demographics of the school population with kids ranging from 6 years to 18 years old.

# How the Application was Built
The basemap was designed by me using the MapBox Style tools and open source tilesets. The base of the map is a common light themed basemap. I layered a Terrain RGB digital elevation model tileset over the basemap in order to show elevations and topography. The terrain has been exaggerated slightly in order to emphasize the topography. I believe the terrain information gives the user the ability to see the innate geographical reality that creates lahar risk in specific communities. Open and gentle valley floors bounded by steep and channeled mountain walls give light to past and future flow patterns. Adding in another terrain vector layer allowed me to staylise the colors of the map and add land use specific colors. The forest land cover is green while the permanently glaciated portions of Mt.Rainier are colored a pale blue.

The lahar risk area is from the USGS Volcano Hazards Program and was created at the Cascade Volcano Observatory in Vancouver, WA. This data was updated in 1998, Hoblit et al(1998), but was originally digitized from a physical mylar greenline map from the USGS Topographic quadrangles. I uploaded the data QGIS and converted the lines from the file into a true polygon and removed the ‘islands’ of higher elevation areas that rise out of but are surrounded by the high risk area. The location of all public schools is available from the Washington State Geospatial portal. A quick clip query in QGIS removes all schools not in the risk area. Both data sets were then converted to GeoJSON and exported for use in the web application. I deleted unnecessary data from the school data and could have applied a simplification query on the risk polygon. Regardless, both files were easily small enough for efficient functionality in the web application. The most difficult part of this process by far was getting proper alignment and projection between the data.

# How the Application Functions
The function of the map is mostly based on the isochrone tutorial from mapbox and utilizes mapbox’s native isochrone API. The main difference being the point is no longer static. A click event initializes the point and calls the isochrone function based on the coordinates selected. Future clicks update the location data and call the isochrone function to recompute. This allows much more interactivity and exploration around the map than in the original tutorial.

Hover for popup information is also included. This relies on a hover event and pulls out information stored in the SchoolsAtRisk.geojson file to display. The popup ability is based on a and feature from the nearest neighbor mapbox tutorial.

# Comments, Concerns, and Possible Additions 
There are a few aspects of the map that should be noted. The traffic data for travel times is obviously an approximation based on data from a normal, non-emergency traffic flow. The travel times also do not take into account the emergency response from first responders that would occur in case of emergency. Many locations have specific evacuation routes planned and some schools have bussing plans to implement in case of emergency.

I would have liked to model this map in 3D to really be able to investigate topographic features that impact lahar flows and emergency evacuations. The mapbox basemap has the ability and it looks quite nice even, however the isochrone api does not function well once the 3D basemap is introduced.

To add to the applications I would have liked to change the lahar risk polygons color scaling. Coloring the area based on predicted travel time from the point of lahar event on Rainier or even just by distance from Rainier would have added a lot of information. Locations downstream have much different evacuation windows than locations positioned closer to the mountain.

While finding distance able to be traveled in a set time from a selected point is nice it would be interesting to find a variable time based on a set distance from a selected point. Ideally the application could tell you the quickest travel time to the nearest safest point from a selected point in the danger zone. This is a combination of nearest neighbor and isochrone functions but was out of the scope of this project.

Next I would add a popup upon loading with a brief description of what the map describes and how to use it. To me it is very intuitive but communicating what the map is depicting and how to use it to a new user seems like a logical

# Information/Data Sources
## For the Curious
https://pubs.usgs.gov/of/2007/1220/data.html
https://blog.mapbox.com/mapbox-cali-terrain-style-bea8cd410523
https://geo.wa.gov/datasets/k12wa::washington-state-public-schools/about
https://www.dnr.wa.gov/publications/ger_ic113_mt_rainier_lahar_hazards.pdf
https://pubs.usgs.gov/of/1998/of98-428/site/CVO%20Website%20-%20Hoblitt,%20et_al_,%201998,%20Volcano%20Hazards%20from%20Mount%20Rainier,%20Washington,%20Revised%201998.htm
https://pubs.usgs.gov/pp/1365/report.pdf
https://www.amazon.com/Classic-Krakauer-Jon-Krakauer-audiobook/dp/B079T9ZRXD/ref=sr_1_2?keywords=collected+essays+by+jon+krakauer&qid=1639281740&s=books&sr=1-2

