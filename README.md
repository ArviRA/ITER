

Skip to content
Using Gmail with screen readers

3 of 284
(no subject)
Inbox
x

Shakileash Chinnaraj <shakileash2000@gmail.com>
Attachments
Sun, Nov 17, 4:01 PM (2 days ago)
to me


Attachments area

import requests
from math import *
def calculate_initial_compass_bearing(pointA, pointB):
    if (type(pointA) != tuple) or (type(pointB) != tuple):
        raise TypeError("Only tuples are supported as arguments")

    lat1 = math.radians(pointA[0])
    lat2 = math.radians(pointB[0])

    diffLong = math.radians(pointB[1] - pointA[1])

    x = math.sin(diffLong) * math.cos(lat2)
    y = math.cos(lat1) * math.sin(lat2) - (math.sin(lat1)
            * math.cos(lat2) * math.cos(diffLong))

    initial_bearing = math.atan2(x, y)
    initial_bearing = math.degrees(initial_bearing)
    compass_bearing = (initial_bearing + 360) % 360

    return compass_bearing
def distance(loc1,loc2):
    R = 6373.0

    lat1 = radians(11.0176)
    lon1 = radians(76.9674)
    lat2 = radians(loc2['lat'])
    lon2 = radians(loc2['lng'])
 
    dlon = lon2 - lon1
    dlat = lat2 - lat1

    a = sin(dlat / 2)**2 + cos(lat1) * cos(lat2) * sin(dlon / 2)**2
    c = 2 * atan2(sqrt(a), sqrt(1 - a))

    distance = R * c

    #print("Result:", distance)
    return distance

 



url_poitoursit='https://maps.googleapis.com/maps/api/place/textsearch/json?query=coimbatore+tourist+attraction+point+of+interest&language=en&radius=50000&key=AIzaSyCn8WMO8Oz0_w6brtx274enxdJnG5bSkUM'
url_malls='https://maps.googleapis.com/maps/api/place/textsearch/json?query=coimbatore+shopping_malls&radius=50000&language=en&key=AIzaSyCn8WMO8Oz0_w6brtx274enxdJnG5bSkUM'
url_hills='https://maps.googleapis.com/maps/api/place/textsearch/json?query=coimbatore+hills&radius=50000&language=en&key=AIzaSyCn8WMO8Oz0_w6brtx274enxdJnG5bSkUM'
url_falls='https://maps.googleapis.com/maps/api/place/textsearch/json?query=coimbatore+waterfalls&radius=50000&language=en&key=AIzaSyCn8WMO8Oz0_w6brtx274enxdJnG5bSkUM'
response=requests.get(url_poitoursit).json()
response1=requests.get(url_malls).json()
response2=requests.get(url_hills).json()
response3=requests.get(url_falls).json()
loc1={'lat':11.0176,'lng':76.9674}
response=response['results']
response1=response1['results']
response2=response2['results']
response3=response3['results']
response.extend(response1)
response.extend(response2)
response.extend(response3)
index=[]
print(len(response))
for k in range(len(response)):
 for j in response[k]['types']:
     if j=="place_of_worship":
           index.append(k)
           print(response[k]['name'],k)
for q in index:
 response=response[0:q-1]+response[q+1:-1]
print(len(response))
for i in range(len(response)):
 
         
 print(response[i]['name'],response[i]['geometry']['location'])
 print(distance(loc1,response[i]['geometry']['location']))
ride.txt
Displaying ride.txt.
