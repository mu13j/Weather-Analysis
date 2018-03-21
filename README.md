
# Observations
* Temperature seems to drop as the absolute value of the latitude gets larger
* Cloudiness and Wind Speed do not appear to have any significant correlation with Latitude
* Cities near the equator tend to have a higher baseline humidity than more polar cities.


```python
import random 
import matplotlib.pyplot as plt
import pandas as pd
from citipy import citipy
import requests
import datetime
```


```python
#Create 500 Random Coordinates
coordinate=[]
for i in range(500):
    a=random.randint(-90,90)
    b=random.randint(-180,180)
    coordinate.append((a,b))
```


```python
#Find City Near the 500 Coordinates
cities = []
for coordinate_pair in coordinate:
    lat, lon = coordinate_pair
    cities.append(citipy.nearest_city(lat, lon))
```


```python
#Find The City Names
citynames=[]
for city in cities:
    citynames.append(city.city_name)
```


```python
#Building URL
url = "http://api.openweathermap.org/data/2.5/weather?"
units = "imperial"
api_key="f8a169f17a1b4378d9a005fa7defdb39"
query_url = f"{url}appid={api_key}&units={units}&q="
```


```python
#Finding Data
temp=[]
lat=[]
humid=[]
cloud=[]
wind=[]
names=[]
for i in range(len(citynames)):
    try:
        name=cities[i].city_name
        query=query_url + citynames[i]
        current_weather=requests.get(query, timeout=30).json()
        lat.append(current_weather['coord']['lat'])
        temp.append(current_weather['main']['temp'])
        humid.append(current_weather['main']['humidity'])
        cloud.append(current_weather['clouds']['all'])
        wind.append(current_weather['wind']['speed'])
        names.append(name)
        print(f'Processing City #{i+1}. ' + f'City name:{name}')
        print(query)
    except KeyError:
        print(f'{name} not found')
        print(query)
```

    Processing City #1. City name:ushuaia
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=ushuaia
    Processing City #2. City name:otavi
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=otavi
    Processing City #3. City name:bluff
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=bluff
    Processing City #4. City name:simao
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=simao
    Processing City #5. City name:isangel
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=isangel
    Processing City #6. City name:ancud
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=ancud
    Processing City #7. City name:ushuaia
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=ushuaia
    Processing City #8. City name:yellowknife
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=yellowknife
    Processing City #9. City name:mnogovershinnyy
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=mnogovershinnyy
    Processing City #10. City name:bluff
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=bluff
    Processing City #11. City name:coihaique
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=coihaique
    Processing City #12. City name:carnarvon
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=carnarvon
    barentsburg not found
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=barentsburg
    Processing City #14. City name:elliot
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=elliot
    Processing City #15. City name:hermanus
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=hermanus
    Processing City #16. City name:beringovskiy
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=beringovskiy
    Processing City #17. City name:vaini
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=vaini
    Processing City #18. City name:bushehr
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=bushehr
    Processing City #19. City name:bilma
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=bilma
    Processing City #20. City name:gamba
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=gamba
    Processing City #21. City name:new norfolk
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=new norfolk
    Processing City #22. City name:jamestown
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=jamestown
    Processing City #23. City name:vaini
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=vaini
    Processing City #24. City name:lukaya
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=lukaya
    illoqqortoormiut not found
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=illoqqortoormiut
    Processing City #26. City name:soto la marina
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=soto la marina
    Processing City #27. City name:hilo
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=hilo
    Processing City #28. City name:mount gambier
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=mount gambier
    Processing City #29. City name:yellowknife
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=yellowknife
    Processing City #30. City name:port hardy
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=port hardy
    Processing City #31. City name:lamu
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=lamu
    Processing City #32. City name:ushuaia
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=ushuaia
    Processing City #33. City name:codrington
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=codrington
    Processing City #34. City name:walvis bay
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=walvis bay
    Processing City #35. City name:jamestown
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=jamestown
    Processing City #36. City name:samarai
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=samarai
    Processing City #37. City name:faanui
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=faanui
    Processing City #38. City name:hilo
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=hilo
    Processing City #39. City name:tessalit
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=tessalit
    Processing City #40. City name:butaritari
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=butaritari
    Processing City #41. City name:albany
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=albany
    Processing City #42. City name:busselton
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=busselton
    Processing City #43. City name:grindavik
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=grindavik
    Processing City #44. City name:georgetown
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=georgetown
    Processing City #45. City name:santa margherita ligure
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=santa margherita ligure
    Processing City #46. City name:rikitea
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=rikitea
    attawapiskat not found
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=attawapiskat
    Processing City #48. City name:ushuaia
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=ushuaia
    Processing City #49. City name:batie
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=batie
    Processing City #50. City name:upernavik
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=upernavik
    Processing City #51. City name:kapaa
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=kapaa
    Processing City #52. City name:ixtapa
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=ixtapa
    Processing City #53. City name:hobart
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=hobart
    Processing City #54. City name:yar-sale
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=yar-sale
    Processing City #55. City name:bluff
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=bluff
    Processing City #56. City name:hermanus
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=hermanus
    Processing City #57. City name:jamestown
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=jamestown
    Processing City #58. City name:oistins
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=oistins
    Processing City #59. City name:petlawad
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=petlawad
    Processing City #60. City name:hobart
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=hobart
    Processing City #61. City name:hermanus
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=hermanus
    Processing City #62. City name:lagoa
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=lagoa
    Processing City #63. City name:severo-kurilsk
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=severo-kurilsk
    Processing City #64. City name:victoria
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=victoria
    Processing City #65. City name:rikitea
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=rikitea
    Processing City #66. City name:formosa
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=formosa
    Processing City #67. City name:ciudad real
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=ciudad real
    Processing City #68. City name:bambous virieux
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=bambous virieux
    Processing City #69. City name:ushuaia
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=ushuaia
    Processing City #70. City name:busselton
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=busselton
    Processing City #71. City name:punta arenas
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=punta arenas
    Processing City #72. City name:lesnoy
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=lesnoy
    Processing City #73. City name:ila
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=ila
    sinkat not found
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=sinkat
    Processing City #75. City name:dikson
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=dikson
    Processing City #76. City name:hermanus
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=hermanus
    Processing City #77. City name:bambous virieux
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=bambous virieux
    tsihombe not found
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=tsihombe
    Processing City #79. City name:roald
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=roald
    Processing City #80. City name:cayambe
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=cayambe
    Processing City #81. City name:geraldton
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=geraldton
    Processing City #82. City name:ouesso
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=ouesso
    Processing City #83. City name:mount gambier
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=mount gambier
    Processing City #84. City name:la reforma
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=la reforma
    Processing City #85. City name:avarua
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=avarua
    Processing City #86. City name:arvika
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=arvika
    Processing City #87. City name:port hawkesbury
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=port hawkesbury
    Processing City #88. City name:ribeira grande
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=ribeira grande
    Processing City #89. City name:mahebourg
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=mahebourg
    grand river south east not found
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=grand river south east
    Processing City #91. City name:ribeira grande
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=ribeira grande
    Processing City #92. City name:ushuaia
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=ushuaia
    santa cruz de rosales not found
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=santa cruz de rosales
    taolanaro not found
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=taolanaro
    Processing City #95. City name:airai
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=airai
    Processing City #96. City name:mataura
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=mataura
    Processing City #97. City name:peace river
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=peace river
    Processing City #98. City name:katsuura
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=katsuura
    Processing City #99. City name:talavera de la reina
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=talavera de la reina
    amderma not found
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=amderma
    Processing City #101. City name:victoria
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=victoria
    Processing City #102. City name:naze
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=naze
    Processing City #103. City name:bathsheba
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=bathsheba
    Processing City #104. City name:flin flon
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=flin flon
    Processing City #105. City name:hilo
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=hilo
    Processing City #106. City name:rikitea
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=rikitea
    Processing City #107. City name:busselton
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=busselton
    Processing City #108. City name:katsuura
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=katsuura
    Processing City #109. City name:souillac
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=souillac
    Processing City #110. City name:mataura
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=mataura
    Processing City #111. City name:port macquarie
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=port macquarie
    Processing City #112. City name:quetta
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=quetta
    Processing City #113. City name:san cristobal
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=san cristobal
    Processing City #114. City name:new norfolk
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=new norfolk
    Processing City #115. City name:butaritari
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=butaritari
    Processing City #116. City name:los llanos de aridane
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=los llanos de aridane
    Processing City #117. City name:batemans bay
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=batemans bay
    Processing City #118. City name:kapaa
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=kapaa
    Processing City #119. City name:komsomolskiy
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=komsomolskiy
    Processing City #120. City name:busselton
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=busselton
    Processing City #121. City name:ushuaia
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=ushuaia
    nguiu not found
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=nguiu
    Processing City #123. City name:kapaa
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=kapaa
    Processing City #124. City name:quatre cocos
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=quatre cocos
    Processing City #125. City name:bredasdorp
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=bredasdorp
    palabuhanratu not found
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=palabuhanratu
    Processing City #127. City name:coquimbo
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=coquimbo
    Processing City #128. City name:kapaa
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=kapaa
    Processing City #129. City name:ushuaia
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=ushuaia
    Processing City #130. City name:teahupoo
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=teahupoo
    Processing City #131. City name:aykhal
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=aykhal
    Processing City #132. City name:tsaratanana
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=tsaratanana
    Processing City #133. City name:pudozh
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=pudozh
    Processing City #134. City name:bluff
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=bluff
    Processing City #135. City name:rikitea
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=rikitea
    Processing City #136. City name:east london
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=east london
    Processing City #137. City name:albany
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=albany
    Processing City #138. City name:jamestown
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=jamestown
    Processing City #139. City name:omsukchan
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=omsukchan
    Processing City #140. City name:avarua
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=avarua
    Processing City #141. City name:severo-kurilsk
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=severo-kurilsk
    Processing City #142. City name:rikitea
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=rikitea
    Processing City #143. City name:nanortalik
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=nanortalik
    Processing City #144. City name:avera
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=avera
    Processing City #145. City name:bandarbeyla
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=bandarbeyla
    nizhneyansk not found
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=nizhneyansk
    Processing City #147. City name:hermanus
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=hermanus
    Processing City #148. City name:ust-maya
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=ust-maya
    Processing City #149. City name:jamestown
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=jamestown
    Processing City #150. City name:albany
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=albany
    Processing City #151. City name:chengde
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=chengde
    Processing City #152. City name:albany
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=albany
    Processing City #153. City name:rikitea
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=rikitea
    Processing City #154. City name:ordu
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=ordu
    Processing City #155. City name:kavieng
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=kavieng
    Processing City #156. City name:luwuk
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=luwuk
    amderma not found
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=amderma
    Processing City #158. City name:bethel
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=bethel
    Processing City #159. City name:hinche
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=hinche
    Processing City #160. City name:hobart
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=hobart
    Processing City #161. City name:tilichiki
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=tilichiki
    Processing City #162. City name:puerto ayora
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=puerto ayora
    Processing City #163. City name:faya
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=faya
    Processing City #164. City name:pevek
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=pevek
    Processing City #165. City name:busselton
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=busselton
    Processing City #166. City name:yellowknife
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=yellowknife
    Processing City #167. City name:butaritari
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=butaritari
    Processing City #168. City name:rikitea
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=rikitea
    Processing City #169. City name:norman wells
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=norman wells
    Processing City #170. City name:cape town
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=cape town
    Processing City #171. City name:ushuaia
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=ushuaia
    Processing City #172. City name:severo-kurilsk
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=severo-kurilsk
    Processing City #173. City name:ushuaia
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=ushuaia
    Processing City #174. City name:rikitea
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=rikitea
    Processing City #175. City name:avarua
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=avarua
    Processing City #176. City name:hermanus
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=hermanus
    Processing City #177. City name:kapaa
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=kapaa
    Processing City #178. City name:bambanglipuro
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=bambanglipuro
    Processing City #179. City name:richards bay
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=richards bay
    Processing City #180. City name:rikitea
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=rikitea
    Processing City #181. City name:san ramon de la nueva oran
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=san ramon de la nueva oran
    Processing City #182. City name:busselton
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=busselton
    Processing City #183. City name:kaitangata
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=kaitangata
    Processing City #184. City name:ploemeur
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=ploemeur
    Processing City #185. City name:amalapuram
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=amalapuram
    tumannyy not found
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=tumannyy
    Processing City #187. City name:bredasdorp
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=bredasdorp
    illoqqortoormiut not found
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=illoqqortoormiut
    Processing City #189. City name:victoria
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=victoria
    Processing City #190. City name:ulladulla
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=ulladulla
    Processing City #191. City name:tiksi
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=tiksi
    Processing City #192. City name:arraial do cabo
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=arraial do cabo
    Processing City #193. City name:luderitz
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=luderitz
    Processing City #194. City name:saint george
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=saint george
    Processing City #195. City name:nouadhibou
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=nouadhibou
    Processing City #196. City name:buala
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=buala
    Processing City #197. City name:kapaa
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=kapaa
    vicuna not found
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=vicuna
    Processing City #199. City name:busselton
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=busselton
    Processing City #200. City name:praia da vitoria
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=praia da vitoria
    marcona not found
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=marcona
    Processing City #202. City name:linxia
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=linxia
    Processing City #203. City name:lata
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=lata
    Processing City #204. City name:chenzhou
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=chenzhou
    Processing City #205. City name:lucapa
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=lucapa
    Processing City #206. City name:hilo
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=hilo
    Processing City #207. City name:hithadhoo
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=hithadhoo
    Processing City #208. City name:port hedland
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=port hedland
    Processing City #209. City name:mar del plata
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=mar del plata
    Processing City #210. City name:trelew
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=trelew
    Processing City #211. City name:mahon
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=mahon
    Processing City #212. City name:souillac
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=souillac
    Processing City #213. City name:nanakuli
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=nanakuli
    Processing City #214. City name:busselton
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=busselton
    Processing City #215. City name:new norfolk
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=new norfolk
    Processing City #216. City name:beloha
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=beloha
    taolanaro not found
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=taolanaro
    Processing City #218. City name:yellowknife
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=yellowknife
    Processing City #219. City name:praia
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=praia
    Processing City #220. City name:bluff
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=bluff
    Processing City #221. City name:vaini
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=vaini
    taolanaro not found
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=taolanaro
    Processing City #223. City name:yulara
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=yulara
    barentsburg not found
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=barentsburg
    Processing City #225. City name:poykovskiy
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=poykovskiy
    Processing City #226. City name:enumclaw
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=enumclaw
    Processing City #227. City name:saint george
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=saint george
    Processing City #228. City name:platteville
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=platteville
    Processing City #229. City name:punta arenas
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=punta arenas
    mys shmidta not found
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=mys shmidta
    Processing City #231. City name:lakes entrance
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=lakes entrance
    Processing City #232. City name:puerto cabello
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=puerto cabello
    Processing City #233. City name:piney green
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=piney green
    Processing City #234. City name:kapaa
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=kapaa
    Processing City #235. City name:dikson
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=dikson
    Processing City #236. City name:jamestown
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=jamestown
    Processing City #237. City name:mazatlan
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=mazatlan
    Processing City #238. City name:khani
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=khani
    Processing City #239. City name:georgetown
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=georgetown
    Processing City #240. City name:lebu
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=lebu
    Processing City #241. City name:hobart
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=hobart
    Processing City #242. City name:salinas
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=salinas
    Processing City #243. City name:ribeira grande
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=ribeira grande
    taolanaro not found
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=taolanaro
    Processing City #245. City name:busselton
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=busselton
    Processing City #246. City name:mataura
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=mataura
    Processing City #247. City name:carnarvon
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=carnarvon
    Processing City #248. City name:bluff
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=bluff
    Processing City #249. City name:porto novo
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=porto novo
    Processing City #250. City name:naze
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=naze
    Processing City #251. City name:rikitea
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=rikitea
    Processing City #252. City name:chokurdakh
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=chokurdakh
    nizhneyansk not found
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=nizhneyansk
    Processing City #254. City name:faanui
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=faanui
    Processing City #255. City name:mataura
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=mataura
    Processing City #256. City name:kanniyakumari
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=kanniyakumari
    Processing City #257. City name:hovd
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=hovd
    Processing City #258. City name:busselton
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=busselton
    tidore not found
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=tidore
    Processing City #260. City name:nantucket
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=nantucket
    Processing City #261. City name:waraseoni
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=waraseoni
    Processing City #262. City name:naze
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=naze
    Processing City #263. City name:mataura
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=mataura
    Processing City #264. City name:bay roberts
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=bay roberts
    Processing City #265. City name:lata
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=lata
    Processing City #266. City name:talnakh
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=talnakh
    Processing City #267. City name:novosil
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=novosil
    Processing City #268. City name:talnakh
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=talnakh
    Processing City #269. City name:albany
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=albany
    Processing City #270. City name:upernavik
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=upernavik
    Processing City #271. City name:punta arenas
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=punta arenas
    Processing City #272. City name:ushuaia
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=ushuaia
    Processing City #273. City name:rawson
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=rawson
    Processing City #274. City name:ngunguru
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=ngunguru
    Processing City #275. City name:jamestown
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=jamestown
    Processing City #276. City name:saskylakh
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=saskylakh
    Processing City #277. City name:kalmunai
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=kalmunai
    Processing City #278. City name:arraial do cabo
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=arraial do cabo
    illoqqortoormiut not found
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=illoqqortoormiut
    Processing City #280. City name:new norfolk
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=new norfolk
    Processing City #281. City name:jalingo
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=jalingo
    Processing City #282. City name:san quintin
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=san quintin
    Processing City #283. City name:mar del plata
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=mar del plata
    Processing City #284. City name:cidreira
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=cidreira
    Processing City #285. City name:san patricio
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=san patricio
    Processing City #286. City name:bluff
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=bluff
    Processing City #287. City name:fort nelson
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=fort nelson
    Processing City #288. City name:busselton
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=busselton
    Processing City #289. City name:dingle
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=dingle
    Processing City #290. City name:port elizabeth
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=port elizabeth
    taolanaro not found
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=taolanaro
    Processing City #292. City name:north vanlaiphai
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=north vanlaiphai
    Processing City #293. City name:laguna
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=laguna
    Processing City #294. City name:terme
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=terme
    Processing City #295. City name:saint-augustin
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=saint-augustin
    Processing City #296. City name:dakar
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=dakar
    Processing City #297. City name:kruisfontein
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=kruisfontein
    Processing City #298. City name:atuona
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=atuona
    Processing City #299. City name:avarua
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=avarua
    Processing City #300. City name:pouso alegre
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=pouso alegre
    Processing City #301. City name:udachnyy
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=udachnyy
    Processing City #302. City name:hobart
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=hobart
    Processing City #303. City name:geraldton
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=geraldton
    Processing City #304. City name:bredasdorp
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=bredasdorp
    Processing City #305. City name:busselton
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=busselton
    tabiauea not found
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=tabiauea
    Processing City #307. City name:lompoc
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=lompoc
    Processing City #308. City name:chuy
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=chuy
    Processing City #309. City name:dikson
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=dikson
    Processing City #310. City name:busselton
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=busselton
    Processing City #311. City name:pevek
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=pevek
    Processing City #312. City name:barrow
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=barrow
    Processing City #313. City name:ponta do sol
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=ponta do sol
    Processing City #314. City name:rikitea
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=rikitea
    illoqqortoormiut not found
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=illoqqortoormiut
    illoqqortoormiut not found
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=illoqqortoormiut
    Processing City #317. City name:qaanaaq
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=qaanaaq
    Processing City #318. City name:fairbanks
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=fairbanks
    Processing City #319. City name:haines junction
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=haines junction
    Processing City #320. City name:turmalina
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=turmalina
    Processing City #321. City name:ponta do sol
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=ponta do sol
    Processing City #322. City name:guarapari
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=guarapari
    Processing City #323. City name:klaksvik
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=klaksvik
    Processing City #324. City name:san juan
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=san juan
    Processing City #325. City name:ponta do sol
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=ponta do sol
    Processing City #326. City name:kapit
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=kapit
    Processing City #327. City name:ushuaia
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=ushuaia
    Processing City #328. City name:butaritari
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=butaritari
    belushya guba not found
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=belushya guba
    Processing City #330. City name:san cristobal
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=san cristobal
    taolanaro not found
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=taolanaro
    Processing City #332. City name:burnie
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=burnie
    Processing City #333. City name:salalah
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=salalah
    Processing City #334. City name:mataura
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=mataura
    Processing City #335. City name:barrow
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=barrow
    Processing City #336. City name:mataura
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=mataura
    omutinskoye not found
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=omutinskoye
    Processing City #338. City name:bereda
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=bereda
    talesh not found
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=talesh
    Processing City #340. City name:isangel
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=isangel
    Processing City #341. City name:butaritari
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=butaritari
    Processing City #342. City name:avarua
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=avarua
    Processing City #343. City name:minna
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=minna
    Processing City #344. City name:annau
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=annau
    mys shmidta not found
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=mys shmidta
    Processing City #346. City name:hami
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=hami
    Processing City #347. City name:bredasdorp
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=bredasdorp
    Processing City #348. City name:geraldton
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=geraldton
    Processing City #349. City name:coquimbo
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=coquimbo
    Processing City #350. City name:oranjemund
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=oranjemund
    Processing City #351. City name:dikson
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=dikson
    Processing City #352. City name:rikitea
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=rikitea
    Processing City #353. City name:merritt
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=merritt
    Processing City #354. City name:adrar
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=adrar
    Processing City #355. City name:nanortalik
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=nanortalik
    Processing City #356. City name:darnah
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=darnah
    Processing City #357. City name:lavrentiya
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=lavrentiya
    Processing City #358. City name:santa cruz cabralia
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=santa cruz cabralia
    Processing City #359. City name:bartica
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=bartica
    Processing City #360. City name:anadyr
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=anadyr
    Processing City #361. City name:punta arenas
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=punta arenas
    Processing City #362. City name:chokurdakh
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=chokurdakh
    Processing City #363. City name:busselton
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=busselton
    Processing City #364. City name:ushuaia
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=ushuaia
    Processing City #365. City name:sitka
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=sitka
    Processing City #366. City name:bredasdorp
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=bredasdorp
    Processing City #367. City name:upernavik
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=upernavik
    Processing City #368. City name:yacuiba
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=yacuiba
    Processing City #369. City name:ponta do sol
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=ponta do sol
    Processing City #370. City name:ganzhou
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=ganzhou
    Processing City #371. City name:sola
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=sola
    Processing City #372. City name:rikitea
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=rikitea
    taolanaro not found
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=taolanaro
    Processing City #374. City name:albany
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=albany
    Processing City #375. City name:rikitea
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=rikitea
    Processing City #376. City name:bathsheba
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=bathsheba
    rolim de moura not found
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=rolim de moura
    Processing City #378. City name:mar del plata
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=mar del plata
    Processing City #379. City name:serenje
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=serenje
    Processing City #380. City name:barra do garcas
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=barra do garcas
    samalaeulu not found
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=samalaeulu
    mys shmidta not found
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=mys shmidta
    Processing City #383. City name:igrim
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=igrim
    Processing City #384. City name:sfantu gheorghe
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=sfantu gheorghe
    cheuskiny not found
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=cheuskiny
    Processing City #386. City name:opuwo
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=opuwo
    Processing City #387. City name:nurota
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=nurota
    Processing City #388. City name:tuatapere
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=tuatapere
    killini not found
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=killini
    Processing City #390. City name:lebu
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=lebu
    Processing City #391. City name:cua
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=cua
    Processing City #392. City name:pryyutivka
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=pryyutivka
    Processing City #393. City name:puerto ayora
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=puerto ayora
    Processing City #394. City name:south lake tahoe
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=south lake tahoe
    Processing City #395. City name:rikitea
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=rikitea
    Processing City #396. City name:busselton
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=busselton
    Processing City #397. City name:bajos de haina
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=bajos de haina
    Processing City #398. City name:port elizabeth
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=port elizabeth
    Processing City #399. City name:hilo
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=hilo
    Processing City #400. City name:remanso
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=remanso
    Processing City #401. City name:lagoa
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=lagoa
    tawnat not found
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=tawnat
    Processing City #403. City name:gizo
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=gizo
    belushya guba not found
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=belushya guba
    Processing City #405. City name:kaitangata
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=kaitangata
    Processing City #406. City name:chambersburg
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=chambersburg
    Processing City #407. City name:busselton
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=busselton
    Processing City #408. City name:yelatma
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=yelatma
    Processing City #409. City name:la ronge
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=la ronge
    Processing City #410. City name:alofi
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=alofi
    Processing City #411. City name:avarua
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=avarua
    Processing City #412. City name:harper
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=harper
    Processing City #413. City name:hobart
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=hobart
    Processing City #414. City name:price
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=price
    Processing City #415. City name:caxito
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=caxito
    Processing City #416. City name:chokurdakh
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=chokurdakh
    Processing City #417. City name:jamestown
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=jamestown
    Processing City #418. City name:fort nelson
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=fort nelson
    Processing City #419. City name:octeville
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=octeville
    Processing City #420. City name:nikolskoye
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=nikolskoye
    Processing City #421. City name:visnes
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=visnes
    Processing City #422. City name:chokurdakh
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=chokurdakh
    Processing City #423. City name:nikolskoye
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=nikolskoye
    Processing City #424. City name:miandrivazo
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=miandrivazo
    Processing City #425. City name:barrow
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=barrow
    Processing City #426. City name:busselton
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=busselton
    Processing City #427. City name:punta arenas
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=punta arenas
    Processing City #428. City name:boulder
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=boulder
    Processing City #429. City name:rikitea
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=rikitea
    Processing City #430. City name:saint-philippe
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=saint-philippe
    Processing City #431. City name:norman wells
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=norman wells
    Processing City #432. City name:abu kamal
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=abu kamal
    Processing City #433. City name:mahebourg
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=mahebourg
    Processing City #434. City name:sangar
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=sangar
    Processing City #435. City name:topolobampo
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=topolobampo
    Processing City #436. City name:saskylakh
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=saskylakh
    Processing City #437. City name:rikitea
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=rikitea
    taolanaro not found
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=taolanaro
    Processing City #439. City name:torbay
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=torbay
    Processing City #440. City name:georgetown
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=georgetown
    Processing City #441. City name:hermanus
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=hermanus
    Processing City #442. City name:lagoa
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=lagoa
    Processing City #443. City name:college
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=college
    Processing City #444. City name:airai
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=airai
    Processing City #445. City name:hermanus
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=hermanus
    Processing City #446. City name:port alfred
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=port alfred
    Processing City #447. City name:dhidhdhoo
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=dhidhdhoo
    Processing City #448. City name:lomza
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=lomza
    Processing City #449. City name:mataura
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=mataura
    Processing City #450. City name:punta arenas
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=punta arenas
    Processing City #451. City name:bilibino
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=bilibino
    Processing City #452. City name:hermanus
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=hermanus
    Processing City #453. City name:bluff
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=bluff
    Processing City #454. City name:busselton
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=busselton
    Processing City #455. City name:mason city
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=mason city
    Processing City #456. City name:provideniya
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=provideniya
    Processing City #457. City name:vaini
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=vaini
    Processing City #458. City name:sinait
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=sinait
    Processing City #459. City name:jinchang
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=jinchang
    Processing City #460. City name:baturaja
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=baturaja
    Processing City #461. City name:yulara
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=yulara
    Processing City #462. City name:kodinsk
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=kodinsk
    Processing City #463. City name:manggar
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=manggar
    Processing City #464. City name:college
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=college
    Processing City #465. City name:chara
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=chara
    illoqqortoormiut not found
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=illoqqortoormiut
    Processing City #467. City name:albany
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=albany
    Processing City #468. City name:san luis
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=san luis
    Processing City #469. City name:tobol
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=tobol
    Processing City #470. City name:dicabisagan
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=dicabisagan
    Processing City #471. City name:ryotsu
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=ryotsu
    Processing City #472. City name:cape town
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=cape town
    Processing City #473. City name:vaini
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=vaini
    Processing City #474. City name:rikitea
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=rikitea
    Processing City #475. City name:pevek
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=pevek
    Processing City #476. City name:punta arenas
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=punta arenas
    Processing City #477. City name:upala
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=upala
    Processing City #478. City name:grand gaube
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=grand gaube
    Processing City #479. City name:bada
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=bada
    Processing City #480. City name:tuktoyaktuk
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=tuktoyaktuk
    Processing City #481. City name:sao filipe
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=sao filipe
    Processing City #482. City name:california city
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=california city
    Processing City #483. City name:rikitea
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=rikitea
    Processing City #484. City name:butaritari
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=butaritari
    Processing City #485. City name:tutoia
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=tutoia
    Processing City #486. City name:karasuk
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=karasuk
    Processing City #487. City name:gallup
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=gallup
    Processing City #488. City name:lorengau
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=lorengau
    Processing City #489. City name:vanavara
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=vanavara
    Processing City #490. City name:saldanha
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=saldanha
    taolanaro not found
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=taolanaro
    Processing City #492. City name:tuktoyaktuk
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=tuktoyaktuk
    Processing City #493. City name:kapuskasing
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=kapuskasing
    Processing City #494. City name:tuatapere
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=tuatapere
    Processing City #495. City name:punta arenas
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=punta arenas
    Processing City #496. City name:hobart
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=hobart
    Processing City #497. City name:mahebourg
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=mahebourg
    Processing City #498. City name:kitale
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=kitale
    Processing City #499. City name:bredasdorp
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=bredasdorp
    Processing City #500. City name:qaanaaq
    http://api.openweathermap.org/data/2.5/weather?appid=f8a169f17a1b4378d9a005fa7defdb39&units=imperial&q=qaanaaq
    


```python
#Exporting CSV
d={'City Name':names,'Temperature':temp,'Latitude':lat,'Humidity':humid,'Cloud %':cloud,'Wind Speed (mph)':wind}
e=pd.DataFrame(d).set_index('City Name')
e.to_csv('output.csv',sep=',')
```


```python
#Temperature Vs Latitude Graph
now = datetime.datetime.now()
plt.scatter(lat,temp)
plt.xlabel('Latitude')
plt.ylabel('Temperature (F)')
plt.title('Temperature vs Latitude ' + now.strftime("%Y-%m-%d"))
plt.grid()
plt.show()
```


![png](output_8_0.png)



```python
#Temperature Vs Humidity Graph
plt.scatter(lat,humid)
plt.grid()
plt.xlabel('Latitude')
plt.ylabel('Humidity')
plt.title('Humidity vs Latitude ' + now.strftime("%Y-%m-%d"))
plt.show()
```


![png](output_9_0.png)



```python
#Temperature vs Cloudiness Graph
plt.scatter(lat,cloud)
plt.xlabel('Latitude')
plt.ylabel('Cloud Cover Percentage')
plt.title('Cloud Cover vs Latitude ' + now.strftime("%Y-%m-%d"))
plt.grid()
plt.show()
```


![png](output_10_0.png)



```python
plt.scatter(lat,wind)
plt.xlabel('Latitude')
plt.ylabel('Wind Speed (MPH)')
plt.title('Wind Speed vs Latitude ' + now.strftime("%Y-%m-%d"))
plt.grid()
plt.show()
```


![png](output_11_0.png)

