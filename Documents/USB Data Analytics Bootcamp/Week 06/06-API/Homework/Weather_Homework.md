

```python
#Dependencies
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt
import requests
import time
import seaborn as sns
import csv
from citipy import citipy
```


```python
#Lat & Longitute
lat_range = (-90,90)
lng_range = (-180,180)
lat_lngs = []
cities = []

lats = np.random.uniform(low=-90.000, high=90.000, size=2000)
lngs = np.random.uniform(low=-180.000, high=180.000, size=2000)
lat_lngs = zip(lats,lngs)

for lat_lng in lat_lngs:
    city = citipy.nearest_city(lat_lng[0],lat_lng[1]).city_name
    
    if city not in cities:
        cities.append(city)
```


```python
#api call
api_key = "ac5bb07823787a1e759cb6180b71b6dc"
url = "http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=" + api_key

city_data = []

record_count = 1
set_count = 1

for i, city in enumerate(cities):
    if(i % 50 == 0 and i >= 50):
        set_count += 1
        record_count = 0
        
    city_url = url + "&q=" + city
    
    print("Processing Record %s of Set %s | %s" % (record_count, set_count, city))
    print(city_url)
    
    record_count += 1
    
    try:
        city_weather = requests.get(city_url).json()
        city_lat = city_weather["coord"]["lat"]
        city_lng = city_weather["coord"]["lon"]
        city_max_temp = city_weather["main"]["temp_max"]
        city_humidity = city_weather["main"]["humidity"]
        city_clouds = city_weather["clouds"]["all"]
        city_wind = city_weather["wind"]["speed"]
        city_country = city_weather["sys"]["country"]
        city_date = city_weather["dt"]
        
        city_data.append({"City": city,
                          "Lat": city_lat,
                          "Lng": city_lng,
                          "Max Temp": city_max_temp,
                          "Humidity": city_humidity,
                          "Cloudiness": city_clouds,
                          "Wind Speed": city_wind,
                          "Country": city_country,
                          "Date": city_date})
    except:
        print("City not found!")
        pass
```

    Processing Record 1 of Set 1 | vaitupu
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=vaitupu
    City not found!
    Processing Record 2 of Set 1 | harwich
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=harwich
    Processing Record 3 of Set 1 | baghdad
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=baghdad
    Processing Record 4 of Set 1 | hermanus
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=hermanus
    Processing Record 5 of Set 1 | santo antonio da platina
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=santo antonio da platina
    Processing Record 6 of Set 1 | atar
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=atar
    Processing Record 7 of Set 1 | atuona
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=atuona
    Processing Record 8 of Set 1 | rikitea
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=rikitea
    Processing Record 9 of Set 1 | taolanaro
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=taolanaro
    City not found!
    Processing Record 10 of Set 1 | hilo
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=hilo
    Processing Record 11 of Set 1 | richards bay
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=richards bay
    Processing Record 12 of Set 1 | ban nahin
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=ban nahin
    Processing Record 13 of Set 1 | kapaa
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=kapaa
    Processing Record 14 of Set 1 | kosonsoy
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=kosonsoy
    Processing Record 15 of Set 1 | bilma
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=bilma
    Processing Record 16 of Set 1 | ushuaia
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=ushuaia
    Processing Record 17 of Set 1 | angoram
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=angoram
    Processing Record 18 of Set 1 | san quintin
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=san quintin
    Processing Record 19 of Set 1 | kigali
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=kigali
    Processing Record 20 of Set 1 | hithadhoo
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=hithadhoo
    Processing Record 21 of Set 1 | khatanga
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=khatanga
    Processing Record 22 of Set 1 | castro
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=castro
    Processing Record 23 of Set 1 | airai
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=airai
    Processing Record 24 of Set 1 | illoqqortoormiut
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=illoqqortoormiut
    City not found!
    Processing Record 25 of Set 1 | cape town
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=cape town
    Processing Record 26 of Set 1 | yellowknife
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=yellowknife
    Processing Record 27 of Set 1 | attawapiskat
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=attawapiskat
    City not found!
    Processing Record 28 of Set 1 | tuktoyaktuk
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=tuktoyaktuk
    Processing Record 29 of Set 1 | chuy
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=chuy
    Processing Record 30 of Set 1 | nikolskoye
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=nikolskoye
    Processing Record 31 of Set 1 | coahuayana
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=coahuayana
    Processing Record 32 of Set 1 | alotau
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=alotau
    City not found!
    Processing Record 33 of Set 1 | isangel
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=isangel
    Processing Record 34 of Set 1 | ribeira grande
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=ribeira grande
    Processing Record 35 of Set 1 | nhulunbuy
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=nhulunbuy
    Processing Record 36 of Set 1 | geraldton
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=geraldton
    Processing Record 37 of Set 1 | barrow
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=barrow
    Processing Record 38 of Set 1 | cabo san lucas
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=cabo san lucas
    Processing Record 39 of Set 1 | victoria
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=victoria
    Processing Record 40 of Set 1 | turochak
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=turochak
    Processing Record 41 of Set 1 | talnakh
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=talnakh
    Processing Record 42 of Set 1 | barentsburg
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=barentsburg
    City not found!
    Processing Record 43 of Set 1 | qaanaaq
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=qaanaaq
    Processing Record 44 of Set 1 | san cristobal
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=san cristobal
    Processing Record 45 of Set 1 | sofiysk
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=sofiysk
    City not found!
    Processing Record 46 of Set 1 | les cayes
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=les cayes
    Processing Record 47 of Set 1 | gamba
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=gamba
    Processing Record 48 of Set 1 | provideniya
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=provideniya
    Processing Record 49 of Set 1 | ahipara
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=ahipara
    Processing Record 50 of Set 1 | punta arenas
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=punta arenas
    Processing Record 0 of Set 2 | kieta
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=kieta
    Processing Record 1 of Set 2 | hendersonville
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=hendersonville
    Processing Record 2 of Set 2 | tsentralnyy
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=tsentralnyy
    City not found!
    Processing Record 3 of Set 2 | caxias do sul
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=caxias do sul
    Processing Record 4 of Set 2 | new norfolk
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=new norfolk
    Processing Record 5 of Set 2 | port alfred
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=port alfred
    Processing Record 6 of Set 2 | pevek
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=pevek
    Processing Record 7 of Set 2 | sentyabrskiy
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=sentyabrskiy
    City not found!
    Processing Record 8 of Set 2 | honolulu
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=honolulu
    Processing Record 9 of Set 2 | moelv
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=moelv
    Processing Record 10 of Set 2 | lahat
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=lahat
    Processing Record 11 of Set 2 | palabuhanratu
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=palabuhanratu
    City not found!
    Processing Record 12 of Set 2 | kuandian
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=kuandian
    Processing Record 13 of Set 2 | lebu
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=lebu
    Processing Record 14 of Set 2 | constitucion
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=constitucion
    Processing Record 15 of Set 2 | bethel
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=bethel
    Processing Record 16 of Set 2 | marystown
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=marystown
    Processing Record 17 of Set 2 | tasiilaq
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=tasiilaq
    Processing Record 18 of Set 2 | mar del plata
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=mar del plata
    Processing Record 19 of Set 2 | severomuysk
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=severomuysk
    Processing Record 20 of Set 2 | upernavik
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=upernavik
    Processing Record 21 of Set 2 | gospic
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=gospic
    Processing Record 22 of Set 2 | carnarvon
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=carnarvon
    Processing Record 23 of Set 2 | bambous virieux
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=bambous virieux
    Processing Record 24 of Set 2 | inhambane
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=inhambane
    Processing Record 25 of Set 2 | comodoro rivadavia
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=comodoro rivadavia
    Processing Record 26 of Set 2 | srivardhan
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=srivardhan
    Processing Record 27 of Set 2 | hasaki
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=hasaki
    Processing Record 28 of Set 2 | tiksi
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=tiksi
    Processing Record 29 of Set 2 | tall kayf
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=tall kayf
    Processing Record 30 of Set 2 | mount gambier
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=mount gambier
    Processing Record 31 of Set 2 | flinders
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=flinders
    Processing Record 32 of Set 2 | shuyskoye
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=shuyskoye
    Processing Record 33 of Set 2 | avarua
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=avarua
    Processing Record 34 of Set 2 | patti
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=patti
    Processing Record 35 of Set 2 | college
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=college
    Processing Record 36 of Set 2 | susurluk
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=susurluk
    Processing Record 37 of Set 2 | bathsheba
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=bathsheba
    Processing Record 38 of Set 2 | kerema
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=kerema
    Processing Record 39 of Set 2 | beaufort
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=beaufort
    Processing Record 40 of Set 2 | tuatapere
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=tuatapere
    Processing Record 41 of Set 2 | salekhard
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=salekhard
    Processing Record 42 of Set 2 | aklavik
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=aklavik
    Processing Record 43 of Set 2 | addi ugri
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=addi ugri
    City not found!
    Processing Record 44 of Set 2 | belushya guba
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=belushya guba
    City not found!
    Processing Record 45 of Set 2 | bengkulu
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=bengkulu
    City not found!
    Processing Record 46 of Set 2 | bialystok
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=bialystok
    Processing Record 47 of Set 2 | ambodifototra
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=ambodifototra
    City not found!
    Processing Record 48 of Set 2 | shimoda
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=shimoda
    Processing Record 49 of Set 2 | bograd
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=bograd
    Processing Record 0 of Set 3 | galiwinku
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=galiwinku
    City not found!
    Processing Record 1 of Set 3 | taburi
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=taburi
    City not found!
    Processing Record 2 of Set 3 | kaitangata
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=kaitangata
    Processing Record 3 of Set 3 | tual
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=tual
    Processing Record 4 of Set 3 | labutta
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=labutta
    City not found!
    Processing Record 5 of Set 3 | udachnyy
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=udachnyy
    Processing Record 6 of Set 3 | zhigansk
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=zhigansk
    Processing Record 7 of Set 3 | kargasok
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=kargasok
    Processing Record 8 of Set 3 | kamenskoye
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=kamenskoye
    City not found!
    Processing Record 9 of Set 3 | kodiak
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=kodiak
    Processing Record 10 of Set 3 | naftah
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=naftah
    City not found!
    Processing Record 11 of Set 3 | marawi
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=marawi
    Processing Record 12 of Set 3 | hobart
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=hobart
    Processing Record 13 of Set 3 | gat
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=gat
    Processing Record 14 of Set 3 | sitka
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=sitka
    Processing Record 15 of Set 3 | komsomolskiy
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=komsomolskiy
    Processing Record 16 of Set 3 | yerbogachen
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=yerbogachen
    Processing Record 17 of Set 3 | yerofey pavlovich
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=yerofey pavlovich
    Processing Record 18 of Set 3 | fiche
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=fiche
    Processing Record 19 of Set 3 | tautira
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=tautira
    Processing Record 20 of Set 3 | clyde river
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=clyde river
    Processing Record 21 of Set 3 | bluff
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=bluff
    Processing Record 22 of Set 3 | bombay
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=bombay
    Processing Record 23 of Set 3 | teneguiban
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=teneguiban
    City not found!
    Processing Record 24 of Set 3 | albany
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=albany
    Processing Record 25 of Set 3 | esperance
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=esperance
    Processing Record 26 of Set 3 | whitecourt
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=whitecourt
    Processing Record 27 of Set 3 | darnah
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=darnah
    Processing Record 28 of Set 3 | afgoye
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=afgoye
    City not found!
    Processing Record 29 of Set 3 | bacuit
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=bacuit
    City not found!
    Processing Record 30 of Set 3 | busselton
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=busselton
    Processing Record 31 of Set 3 | arraial do cabo
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=arraial do cabo
    Processing Record 32 of Set 3 | gidole
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=gidole
    Processing Record 33 of Set 3 | solnechnyy
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=solnechnyy
    Processing Record 34 of Set 3 | berezovyy
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=berezovyy
    Processing Record 35 of Set 3 | bredasdorp
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=bredasdorp
    Processing Record 36 of Set 3 | thompson
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=thompson
    Processing Record 37 of Set 3 | copiapo
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=copiapo
    Processing Record 38 of Set 3 | saint-joseph
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=saint-joseph
    Processing Record 39 of Set 3 | saleaula
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=saleaula
    City not found!
    Processing Record 40 of Set 3 | vaini
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=vaini
    Processing Record 41 of Set 3 | den helder
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=den helder
    Processing Record 42 of Set 3 | sola
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=sola
    Processing Record 43 of Set 3 | byron bay
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=byron bay
    Processing Record 44 of Set 3 | tari
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=tari
    Processing Record 45 of Set 3 | tura
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=tura
    Processing Record 46 of Set 3 | babanusah
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=babanusah
    City not found!
    Processing Record 47 of Set 3 | mehamn
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=mehamn
    Processing Record 48 of Set 3 | sovetskiy
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=sovetskiy
    Processing Record 49 of Set 3 | port lincoln
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=port lincoln
    Processing Record 0 of Set 4 | metkovic
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=metkovic
    Processing Record 1 of Set 4 | guozhen
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=guozhen
    Processing Record 2 of Set 4 | kaele
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=kaele
    Processing Record 3 of Set 4 | tarudant
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=tarudant
    City not found!
    Processing Record 4 of Set 4 | jumla
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=jumla
    Processing Record 5 of Set 4 | hofn
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=hofn
    Processing Record 6 of Set 4 | mataura
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=mataura
    Processing Record 7 of Set 4 | tsihombe
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=tsihombe
    City not found!
    Processing Record 8 of Set 4 | lagoa
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=lagoa
    Processing Record 9 of Set 4 | saskylakh
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=saskylakh
    Processing Record 10 of Set 4 | sibu
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=sibu
    Processing Record 11 of Set 4 | kavaratti
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=kavaratti
    Processing Record 12 of Set 4 | a
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=a
    City not found!
    Processing Record 13 of Set 4 | hamilton
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=hamilton
    Processing Record 14 of Set 4 | jalu
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=jalu
    Processing Record 15 of Set 4 | nemuro
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=nemuro
    Processing Record 16 of Set 4 | torbay
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=torbay
    Processing Record 17 of Set 4 | tumannyy
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=tumannyy
    City not found!
    Processing Record 18 of Set 4 | barkhan
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=barkhan
    Processing Record 19 of Set 4 | cravo norte
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=cravo norte
    Processing Record 20 of Set 4 | kyzyl-suu
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=kyzyl-suu
    Processing Record 21 of Set 4 | preobrazheniye
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=preobrazheniye
    Processing Record 22 of Set 4 | mahibadhoo
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=mahibadhoo
    Processing Record 23 of Set 4 | japura
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=japura
    Processing Record 24 of Set 4 | butaritari
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=butaritari
    Processing Record 25 of Set 4 | felidhoo
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=felidhoo
    City not found!
    Processing Record 26 of Set 4 | camacha
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=camacha
    Processing Record 27 of Set 4 | nizhneyansk
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=nizhneyansk
    City not found!
    Processing Record 28 of Set 4 | lahij
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=lahij
    Processing Record 29 of Set 4 | kungurtug
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=kungurtug
    Processing Record 30 of Set 4 | solin
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=solin
    Processing Record 31 of Set 4 | port hardy
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=port hardy
    Processing Record 32 of Set 4 | makushino
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=makushino
    Processing Record 33 of Set 4 | zambrow
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=zambrow
    Processing Record 34 of Set 4 | mglin
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=mglin
    Processing Record 35 of Set 4 | lere
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=lere
    Processing Record 36 of Set 4 | port moresby
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=port moresby
    Processing Record 37 of Set 4 | osakarovka
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=osakarovka
    Processing Record 38 of Set 4 | sao benedito do rio preto
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=sao benedito do rio preto
    Processing Record 39 of Set 4 | koumac
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=koumac
    Processing Record 40 of Set 4 | santa flavia
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=santa flavia
    Processing Record 41 of Set 4 | kasese
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=kasese
    Processing Record 42 of Set 4 | codrington
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=codrington
    Processing Record 43 of Set 4 | henties bay
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=henties bay
    Processing Record 44 of Set 4 | longyearbyen
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=longyearbyen
    Processing Record 45 of Set 4 | karwar
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=karwar
    Processing Record 46 of Set 4 | plettenberg bay
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=plettenberg bay
    Processing Record 47 of Set 4 | villazon
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=villazon
    City not found!
    Processing Record 48 of Set 4 | dikson
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=dikson
    Processing Record 49 of Set 4 | meulaboh
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=meulaboh
    Processing Record 0 of Set 5 | eyl
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=eyl
    Processing Record 1 of Set 5 | egvekinot
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=egvekinot
    Processing Record 2 of Set 5 | saldanha
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=saldanha
    Processing Record 3 of Set 5 | jamestown
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=jamestown
    Processing Record 4 of Set 5 | bowen
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=bowen
    Processing Record 5 of Set 5 | lorengau
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=lorengau
    Processing Record 6 of Set 5 | terra santa
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=terra santa
    Processing Record 7 of Set 5 | georgetown
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=georgetown
    Processing Record 8 of Set 5 | balimo
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=balimo
    City not found!
    Processing Record 9 of Set 5 | nieuw nickerie
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=nieuw nickerie
    Processing Record 10 of Set 5 | ancud
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=ancud
    Processing Record 11 of Set 5 | klaksvik
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=klaksvik
    Processing Record 12 of Set 5 | caravelas
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=caravelas
    Processing Record 13 of Set 5 | tarauaca
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=tarauaca
    Processing Record 14 of Set 5 | la rioja
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=la rioja
    Processing Record 15 of Set 5 | otofuke
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=otofuke
    Processing Record 16 of Set 5 | grindavik
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=grindavik
    Processing Record 17 of Set 5 | lehututu
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=lehututu
    Processing Record 18 of Set 5 | bandar penggaram
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=bandar penggaram
    City not found!
    Processing Record 19 of Set 5 | xiongzhou
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=xiongzhou
    Processing Record 20 of Set 5 | moranbah
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=moranbah
    Processing Record 21 of Set 5 | wadi maliz
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=wadi maliz
    Processing Record 22 of Set 5 | mpika
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=mpika
    Processing Record 23 of Set 5 | discovery bay
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=discovery bay
    Processing Record 24 of Set 5 | saint-philippe
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=saint-philippe
    Processing Record 25 of Set 5 | tessalit
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=tessalit
    Processing Record 26 of Set 5 | la asuncion
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=la asuncion
    Processing Record 27 of Set 5 | severo-kurilsk
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=severo-kurilsk
    Processing Record 28 of Set 5 | ponta delgada
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=ponta delgada
    Processing Record 29 of Set 5 | pilar
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=pilar
    Processing Record 30 of Set 5 | okhotsk
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=okhotsk
    Processing Record 31 of Set 5 | aksha
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=aksha
    Processing Record 32 of Set 5 | oktyabrskoye
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=oktyabrskoye
    Processing Record 33 of Set 5 | am timan
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=am timan
    Processing Record 34 of Set 5 | seredka
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=seredka
    Processing Record 35 of Set 5 | wahran
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=wahran
    City not found!
    Processing Record 36 of Set 5 | faya
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=faya
    Processing Record 37 of Set 5 | ostrovnoy
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=ostrovnoy
    Processing Record 38 of Set 5 | karamea
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=karamea
    City not found!
    Processing Record 39 of Set 5 | faanui
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=faanui
    Processing Record 40 of Set 5 | port elizabeth
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=port elizabeth
    Processing Record 41 of Set 5 | port macquarie
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=port macquarie
    Processing Record 42 of Set 5 | rungata
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=rungata
    City not found!
    Processing Record 43 of Set 5 | hambantota
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=hambantota
    Processing Record 44 of Set 5 | naze
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=naze
    Processing Record 45 of Set 5 | iskilip
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=iskilip
    Processing Record 46 of Set 5 | mahajanga
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=mahajanga
    Processing Record 47 of Set 5 | berlevag
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=berlevag
    Processing Record 48 of Set 5 | katsuura
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=katsuura
    Processing Record 49 of Set 5 | abbeville
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=abbeville
    Processing Record 0 of Set 6 | katobu
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=katobu
    Processing Record 1 of Set 6 | puerto armuelles
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=puerto armuelles
    Processing Record 2 of Set 6 | iquique
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=iquique
    Processing Record 3 of Set 6 | atikokan
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=atikokan
    Processing Record 4 of Set 6 | mayumba
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=mayumba
    Processing Record 5 of Set 6 | estelle
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=estelle
    Processing Record 6 of Set 6 | mahebourg
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=mahebourg
    Processing Record 7 of Set 6 | maiduguri
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=maiduguri
    Processing Record 8 of Set 6 | hamakita
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=hamakita
    Processing Record 9 of Set 6 | skibbereen
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=skibbereen
    Processing Record 10 of Set 6 | port shepstone
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=port shepstone
    Processing Record 11 of Set 6 | mount isa
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=mount isa
    Processing Record 12 of Set 6 | jardim
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=jardim
    Processing Record 13 of Set 6 | jos
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=jos
    Processing Record 14 of Set 6 | santiago del estero
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=santiago del estero
    Processing Record 15 of Set 6 | mys shmidta
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=mys shmidta
    City not found!
    Processing Record 16 of Set 6 | asau
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=asau
    City not found!
    Processing Record 17 of Set 6 | magistralnyy
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=magistralnyy
    Processing Record 18 of Set 6 | vardo
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=vardo
    Processing Record 19 of Set 6 | honningsvag
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=honningsvag
    Processing Record 20 of Set 6 | coquimbo
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=coquimbo
    Processing Record 21 of Set 6 | amderma
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=amderma
    City not found!
    Processing Record 22 of Set 6 | lagunillas
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=lagunillas
    Processing Record 23 of Set 6 | farafangana
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=farafangana
    Processing Record 24 of Set 6 | saint george
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=saint george
    Processing Record 25 of Set 6 | lebedinyy
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=lebedinyy
    Processing Record 26 of Set 6 | westport
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=westport
    Processing Record 27 of Set 6 | colac
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=colac
    Processing Record 28 of Set 6 | alleroy
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=alleroy
    Processing Record 29 of Set 6 | canon city
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=canon city
    Processing Record 30 of Set 6 | beaverlodge
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=beaverlodge
    Processing Record 31 of Set 6 | tatawin
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=tatawin
    City not found!
    Processing Record 32 of Set 6 | paraopeba
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=paraopeba
    Processing Record 33 of Set 6 | ossora
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=ossora
    Processing Record 34 of Set 6 | slave lake
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=slave lake
    Processing Record 35 of Set 6 | najran
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=najran
    Processing Record 36 of Set 6 | port blair
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=port blair
    Processing Record 37 of Set 6 | tera
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=tera
    Processing Record 38 of Set 6 | meiganga
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=meiganga
    Processing Record 39 of Set 6 | pelym
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=pelym
    Processing Record 40 of Set 6 | fortuna
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=fortuna
    Processing Record 41 of Set 6 | kirakira
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=kirakira
    Processing Record 42 of Set 6 | cherskiy
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=cherskiy
    Processing Record 43 of Set 6 | acapulco
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=acapulco
    Processing Record 44 of Set 6 | saint anthony
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=saint anthony
    Processing Record 45 of Set 6 | itoman
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=itoman
    Processing Record 46 of Set 6 | puerto ayora
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=puerto ayora
    Processing Record 47 of Set 6 | kisaran
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=kisaran
    Processing Record 48 of Set 6 | marzuq
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=marzuq
    Processing Record 49 of Set 6 | kaitong
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=kaitong
    Processing Record 0 of Set 7 | lasa
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=lasa
    Processing Record 1 of Set 7 | sidrolandia
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=sidrolandia
    Processing Record 2 of Set 7 | dingle
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=dingle
    Processing Record 3 of Set 7 | kamina
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=kamina
    Processing Record 4 of Set 7 | eregli
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=eregli
    Processing Record 5 of Set 7 | severobaykalsk
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=severobaykalsk
    Processing Record 6 of Set 7 | garrel
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=garrel
    Processing Record 7 of Set 7 | port arthur
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=port arthur
    Processing Record 8 of Set 7 | saint-augustin
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=saint-augustin
    Processing Record 9 of Set 7 | umea
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=umea
    Processing Record 10 of Set 7 | bereda
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=bereda
    Processing Record 11 of Set 7 | kerki
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=kerki
    City not found!
    Processing Record 12 of Set 7 | sur
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=sur
    Processing Record 13 of Set 7 | bandarbeyla
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=bandarbeyla
    Processing Record 14 of Set 7 | vieques
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=vieques
    Processing Record 15 of Set 7 | mamallapuram
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=mamallapuram
    Processing Record 16 of Set 7 | labuan
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=labuan
    Processing Record 17 of Set 7 | burica
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=burica
    City not found!
    Processing Record 18 of Set 7 | east london
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=east london
    Processing Record 19 of Set 7 | san ramon
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=san ramon
    Processing Record 20 of Set 7 | rorvik
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=rorvik
    Processing Record 21 of Set 7 | necochea
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=necochea
    Processing Record 22 of Set 7 | balud
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=balud
    Processing Record 23 of Set 7 | okha
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=okha
    Processing Record 24 of Set 7 | lavrentiya
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=lavrentiya
    Processing Record 25 of Set 7 | starodub
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=starodub
    Processing Record 26 of Set 7 | namibe
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=namibe
    Processing Record 27 of Set 7 | samfya
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=samfya
    Processing Record 28 of Set 7 | claudio
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=claudio
    Processing Record 29 of Set 7 | alpena
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=alpena
    Processing Record 30 of Set 7 | hirara
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=hirara
    Processing Record 31 of Set 7 | itarema
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=itarema
    Processing Record 32 of Set 7 | buraydah
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=buraydah
    Processing Record 33 of Set 7 | cartagena
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=cartagena
    Processing Record 34 of Set 7 | eunice
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=eunice
    Processing Record 35 of Set 7 | poum
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=poum
    Processing Record 36 of Set 7 | kloulklubed
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=kloulklubed
    Processing Record 37 of Set 7 | antofagasta
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=antofagasta
    Processing Record 38 of Set 7 | dengzhou
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=dengzhou
    Processing Record 39 of Set 7 | xining
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=xining
    Processing Record 40 of Set 7 | carquefou
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=carquefou
    Processing Record 41 of Set 7 | buala
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=buala
    Processing Record 42 of Set 7 | sistranda
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=sistranda
    Processing Record 43 of Set 7 | jorhat
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=jorhat
    Processing Record 44 of Set 7 | tazovskiy
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=tazovskiy
    Processing Record 45 of Set 7 | kongolo
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=kongolo
    Processing Record 46 of Set 7 | pringsewu
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=pringsewu
    Processing Record 47 of Set 7 | chagda
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=chagda
    City not found!
    Processing Record 48 of Set 7 | labuhan
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=labuhan
    Processing Record 49 of Set 7 | makakilo city
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=makakilo city
    Processing Record 0 of Set 8 | inongo
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=inongo
    Processing Record 1 of Set 8 | xiongshi
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=xiongshi
    City not found!
    Processing Record 2 of Set 8 | panguna
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=panguna
    Processing Record 3 of Set 8 | bellefontaine
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=bellefontaine
    Processing Record 4 of Set 8 | inuvik
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=inuvik
    Processing Record 5 of Set 8 | prado
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=prado
    Processing Record 6 of Set 8 | catalao
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=catalao
    Processing Record 7 of Set 8 | liverpool
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=liverpool
    Processing Record 8 of Set 8 | along
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=along
    Processing Record 9 of Set 8 | thomaston
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=thomaston
    Processing Record 10 of Set 8 | kampot
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=kampot
    Processing Record 11 of Set 8 | los llanos de aridane
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=los llanos de aridane
    Processing Record 12 of Set 8 | jumilla
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=jumilla
    Processing Record 13 of Set 8 | sorvag
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=sorvag
    City not found!
    Processing Record 14 of Set 8 | luderitz
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=luderitz
    Processing Record 15 of Set 8 | wangkui
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=wangkui
    Processing Record 16 of Set 8 | pacific grove
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=pacific grove
    Processing Record 17 of Set 8 | marcona
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=marcona
    City not found!
    Processing Record 18 of Set 8 | salalah
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=salalah
    Processing Record 19 of Set 8 | sloboda
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=sloboda
    Processing Record 20 of Set 8 | tateyama
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=tateyama
    Processing Record 21 of Set 8 | dehloran
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=dehloran
    Processing Record 22 of Set 8 | suarez
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=suarez
    Processing Record 23 of Set 8 | plover
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=plover
    Processing Record 24 of Set 8 | pangnirtung
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=pangnirtung
    Processing Record 25 of Set 8 | bulaevo
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=bulaevo
    Processing Record 26 of Set 8 | dalvik
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=dalvik
    Processing Record 27 of Set 8 | bayir
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=bayir
    Processing Record 28 of Set 8 | sarangani
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=sarangani
    Processing Record 29 of Set 8 | amuntai
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=amuntai
    Processing Record 30 of Set 8 | seoul
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=seoul
    Processing Record 31 of Set 8 | bonnyville
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=bonnyville
    Processing Record 32 of Set 8 | grootegast
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=grootegast
    Processing Record 33 of Set 8 | mtama
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=mtama
    Processing Record 34 of Set 8 | cuenca
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=cuenca
    Processing Record 35 of Set 8 | redmond
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=redmond
    Processing Record 36 of Set 8 | nanortalik
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=nanortalik
    Processing Record 37 of Set 8 | hualmay
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=hualmay
    Processing Record 38 of Set 8 | parana
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=parana
    Processing Record 39 of Set 8 | wanaka
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=wanaka
    Processing Record 40 of Set 8 | novoilinsk
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=novoilinsk
    City not found!
    Processing Record 41 of Set 8 | amargosa
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=amargosa
    Processing Record 42 of Set 8 | grand centre
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=grand centre
    City not found!
    Processing Record 43 of Set 8 | ijaki
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=ijaki
    City not found!
    Processing Record 44 of Set 8 | souillac
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=souillac
    Processing Record 45 of Set 8 | taft
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=taft
    Processing Record 46 of Set 8 | broken hill
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=broken hill
    Processing Record 47 of Set 8 | zhezkazgan
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=zhezkazgan
    Processing Record 48 of Set 8 | gilgit
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=gilgit
    Processing Record 49 of Set 8 | beringovskiy
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=beringovskiy
    Processing Record 0 of Set 9 | dunedin
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=dunedin
    Processing Record 1 of Set 9 | jaisinghnagar
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=jaisinghnagar
    Processing Record 2 of Set 9 | caarapo
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=caarapo
    Processing Record 3 of Set 9 | tagusao
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=tagusao
    Processing Record 4 of Set 9 | kushima
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=kushima
    Processing Record 5 of Set 9 | soyo
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=soyo
    Processing Record 6 of Set 9 | saint-pierre
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=saint-pierre
    Processing Record 7 of Set 9 | ormara
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=ormara
    Processing Record 8 of Set 9 | winnemucca
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=winnemucca
    Processing Record 9 of Set 9 | cidreira
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=cidreira
    Processing Record 10 of Set 9 | avanigadda
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=avanigadda
    Processing Record 11 of Set 9 | tawnat
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=tawnat
    City not found!
    Processing Record 12 of Set 9 | omboue
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=omboue
    Processing Record 13 of Set 9 | oyama
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=oyama
    Processing Record 14 of Set 9 | hay river
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=hay river
    Processing Record 15 of Set 9 | malangali
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=malangali
    Processing Record 16 of Set 9 | pangai
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=pangai
    Processing Record 17 of Set 9 | borujerd
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=borujerd
    Processing Record 18 of Set 9 | mattru
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=mattru
    Processing Record 19 of Set 9 | zaozerne
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=zaozerne
    Processing Record 20 of Set 9 | lolua
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=lolua
    City not found!
    Processing Record 21 of Set 9 | russell
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=russell
    Processing Record 22 of Set 9 | bubaque
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=bubaque
    Processing Record 23 of Set 9 | yaan
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=yaan
    Processing Record 24 of Set 9 | yulara
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=yulara
    Processing Record 25 of Set 9 | bytow
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=bytow
    Processing Record 26 of Set 9 | mayo
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=mayo
    Processing Record 27 of Set 9 | impfondo
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=impfondo
    Processing Record 28 of Set 9 | ta khmau
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=ta khmau
    Processing Record 29 of Set 9 | alamos
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=alamos
    Processing Record 30 of Set 9 | korla
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=korla
    City not found!
    Processing Record 31 of Set 9 | santa maria
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=santa maria
    Processing Record 32 of Set 9 | ca mau
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=ca mau
    Processing Record 33 of Set 9 | chontalpa
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=chontalpa
    Processing Record 34 of Set 9 | parnamirim
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=parnamirim
    Processing Record 35 of Set 9 | magadan
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=magadan
    Processing Record 36 of Set 9 | yumen
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=yumen
    Processing Record 37 of Set 9 | kruisfontein
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=kruisfontein
    Processing Record 38 of Set 9 | emerald
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=emerald
    Processing Record 39 of Set 9 | gizo
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=gizo
    Processing Record 40 of Set 9 | teya
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=teya
    Processing Record 41 of Set 9 | sao joao da barra
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=sao joao da barra
    Processing Record 42 of Set 9 | haverfordwest
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=haverfordwest
    Processing Record 43 of Set 9 | zeya
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=zeya
    Processing Record 44 of Set 9 | phrai bung
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=phrai bung
    City not found!
    Processing Record 45 of Set 9 | sabang
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=sabang
    Processing Record 46 of Set 9 | grand gaube
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=grand gaube
    Processing Record 47 of Set 9 | vysokogornyy
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=vysokogornyy
    Processing Record 48 of Set 9 | anadyr
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=anadyr
    Processing Record 49 of Set 9 | vathi
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=vathi
    Processing Record 0 of Set 10 | flin flon
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=flin flon
    Processing Record 1 of Set 10 | aasiaat
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=aasiaat
    Processing Record 2 of Set 10 | lahaina
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=lahaina
    Processing Record 3 of Set 10 | drumheller
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=drumheller
    Processing Record 4 of Set 10 | kaili
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=kaili
    Processing Record 5 of Set 10 | bosaso
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=bosaso
    Processing Record 6 of Set 10 | lhuntshi
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=lhuntshi
    City not found!
    Processing Record 7 of Set 10 | alta floresta
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=alta floresta
    Processing Record 8 of Set 10 | narrabri
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=narrabri
    Processing Record 9 of Set 10 | oktyabrskiy
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=oktyabrskiy
    Processing Record 10 of Set 10 | lagdo
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=lagdo
    Processing Record 11 of Set 10 | guerrero negro
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=guerrero negro
    Processing Record 12 of Set 10 | sioux lookout
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=sioux lookout
    Processing Record 13 of Set 10 | hailun
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=hailun
    Processing Record 14 of Set 10 | fairbanks
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=fairbanks
    Processing Record 15 of Set 10 | la ronge
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=la ronge
    Processing Record 16 of Set 10 | kimberley
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=kimberley
    Processing Record 17 of Set 10 | hillsborough
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=hillsborough
    Processing Record 18 of Set 10 | alice springs
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=alice springs
    Processing Record 19 of Set 10 | sao felix do xingu
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=sao felix do xingu
    Processing Record 20 of Set 10 | leningradskiy
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=leningradskiy
    Processing Record 21 of Set 10 | orel-izumrud
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=orel-izumrud
    Processing Record 22 of Set 10 | grand river south east
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=grand river south east
    City not found!
    Processing Record 23 of Set 10 | north platte
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=north platte
    Processing Record 24 of Set 10 | bukachacha
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=bukachacha
    Processing Record 25 of Set 10 | vestbygda
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=vestbygda
    City not found!
    Processing Record 26 of Set 10 | ulan-ude
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=ulan-ude
    Processing Record 27 of Set 10 | utiroa
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=utiroa
    City not found!
    Processing Record 28 of Set 10 | rodrigues alves
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=rodrigues alves
    Processing Record 29 of Set 10 | kaka
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=kaka
    Processing Record 30 of Set 10 | valencia
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=valencia
    Processing Record 31 of Set 10 | gweta
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=gweta
    Processing Record 32 of Set 10 | kaoma
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=kaoma
    Processing Record 33 of Set 10 | vanavara
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=vanavara
    Processing Record 34 of Set 10 | turukhansk
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=turukhansk
    Processing Record 35 of Set 10 | yomitan
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=yomitan
    City not found!
    Processing Record 36 of Set 10 | susangerd
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=susangerd
    Processing Record 37 of Set 10 | dauriya
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=dauriya
    Processing Record 38 of Set 10 | bethanien
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=bethanien
    Processing Record 39 of Set 10 | san vicente
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=san vicente
    Processing Record 40 of Set 10 | dagumba-an
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=dagumba-an
    Processing Record 41 of Set 10 | vedaranniyam
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=vedaranniyam
    City not found!
    Processing Record 42 of Set 10 | horadiz
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=horadiz
    Processing Record 43 of Set 10 | guadalupe
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=guadalupe
    Processing Record 44 of Set 10 | batemans bay
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=batemans bay
    Processing Record 45 of Set 10 | maniitsoq
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=maniitsoq
    Processing Record 46 of Set 10 | curillo
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=curillo
    Processing Record 47 of Set 10 | touros
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=touros
    Processing Record 48 of Set 10 | samusu
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=samusu
    City not found!
    Processing Record 49 of Set 10 | mocuba
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=mocuba
    Processing Record 0 of Set 11 | sambava
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=sambava
    Processing Record 1 of Set 11 | bloemhof
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=bloemhof
    Processing Record 2 of Set 11 | vao
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=vao
    Processing Record 3 of Set 11 | merauke
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=merauke
    Processing Record 4 of Set 11 | talcahuano
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=talcahuano
    Processing Record 5 of Set 11 | palmer
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=palmer
    Processing Record 6 of Set 11 | dumas
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=dumas
    Processing Record 7 of Set 11 | cayenne
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=cayenne
    Processing Record 8 of Set 11 | abu dhabi
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=abu dhabi
    Processing Record 9 of Set 11 | shelburne
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=shelburne
    Processing Record 10 of Set 11 | waxahachie
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=waxahachie
    Processing Record 11 of Set 11 | mnogovershinnyy
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=mnogovershinnyy
    Processing Record 12 of Set 11 | coihaique
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=coihaique
    Processing Record 13 of Set 11 | enshi
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=enshi
    Processing Record 14 of Set 11 | carsamba
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=carsamba
    Processing Record 15 of Set 11 | mattawa
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=mattawa
    Processing Record 16 of Set 11 | houma
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=houma
    Processing Record 17 of Set 11 | severo-yeniseyskiy
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=severo-yeniseyskiy
    Processing Record 18 of Set 11 | matagami
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=matagami
    Processing Record 19 of Set 11 | baishishan
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=baishishan
    Processing Record 20 of Set 11 | bababe
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=bababe
    City not found!
    Processing Record 21 of Set 11 | ibra
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=ibra
    Processing Record 22 of Set 11 | marathon
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=marathon
    Processing Record 23 of Set 11 | aswan
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=aswan
    Processing Record 24 of Set 11 | tezu
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=tezu
    Processing Record 25 of Set 11 | samarai
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=samarai
    Processing Record 26 of Set 11 | san carlos de bariloche
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=san carlos de bariloche
    Processing Record 27 of Set 11 | ilulissat
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=ilulissat
    Processing Record 28 of Set 11 | marsh harbour
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=marsh harbour
    Processing Record 29 of Set 11 | rincon de la victoria
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=rincon de la victoria
    Processing Record 30 of Set 11 | cuiluan
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=cuiluan
    Processing Record 31 of Set 11 | kulhudhuffushi
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=kulhudhuffushi
    Processing Record 32 of Set 11 | cayambe
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=cayambe
    Processing Record 33 of Set 11 | weligama
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=weligama
    Processing Record 34 of Set 11 | san patricio
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=san patricio
    Processing Record 35 of Set 11 | tukrah
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=tukrah
    City not found!
    Processing Record 36 of Set 11 | kpandae
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=kpandae
    Processing Record 37 of Set 11 | iqaluit
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=iqaluit
    Processing Record 38 of Set 11 | myszkow
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=myszkow
    Processing Record 39 of Set 11 | celestun
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=celestun
    Processing Record 40 of Set 11 | nome
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=nome
    Processing Record 41 of Set 11 | bira
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=bira
    Processing Record 42 of Set 11 | ingham
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=ingham
    Processing Record 43 of Set 11 | nkhotakota
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=nkhotakota
    Processing Record 44 of Set 11 | sao filipe
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=sao filipe
    Processing Record 45 of Set 11 | sylacauga
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=sylacauga
    Processing Record 46 of Set 11 | veraval
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=veraval
    Processing Record 47 of Set 11 | murakami
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=murakami
    Processing Record 48 of Set 11 | kuche
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=kuche
    City not found!
    Processing Record 49 of Set 11 | mpongwe
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=mpongwe
    Processing Record 0 of Set 12 | karpuninskiy
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=karpuninskiy
    City not found!
    Processing Record 1 of Set 12 | portland
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=portland
    Processing Record 2 of Set 12 | mao
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=mao
    Processing Record 3 of Set 12 | warqla
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=warqla
    City not found!
    Processing Record 4 of Set 12 | dukat
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=dukat
    Processing Record 5 of Set 12 | sidi bu zayd
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=sidi bu zayd
    City not found!
    Processing Record 6 of Set 12 | tlaxco
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=tlaxco
    Processing Record 7 of Set 12 | raudeberg
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=raudeberg
    Processing Record 8 of Set 12 | alofi
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=alofi
    Processing Record 9 of Set 12 | port-gentil
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=port-gentil
    Processing Record 10 of Set 12 | ramnagar
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=ramnagar
    Processing Record 11 of Set 12 | amahai
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=amahai
    Processing Record 12 of Set 12 | maur
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=maur
    Processing Record 13 of Set 12 | ayan
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=ayan
    Processing Record 14 of Set 12 | patnagarh
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=patnagarh
    Processing Record 15 of Set 12 | lompoc
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=lompoc
    Processing Record 16 of Set 12 | dicabisagan
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=dicabisagan
    Processing Record 17 of Set 12 | alice
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=alice
    Processing Record 18 of Set 12 | mackay
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=mackay
    Processing Record 19 of Set 12 | barentu
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=barentu
    Processing Record 20 of Set 12 | manakara
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=manakara
    Processing Record 21 of Set 12 | nsanje
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=nsanje
    Processing Record 22 of Set 12 | kytlym
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=kytlym
    City not found!
    Processing Record 23 of Set 12 | hatillo
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=hatillo
    Processing Record 24 of Set 12 | edd
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=edd
    Processing Record 25 of Set 12 | geilo
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=geilo
    Processing Record 26 of Set 12 | pisco
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=pisco
    Processing Record 27 of Set 12 | pierre
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=pierre
    Processing Record 28 of Set 12 | mastic beach
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=mastic beach
    Processing Record 29 of Set 12 | rundu
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=rundu
    Processing Record 30 of Set 12 | castanos
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=castanos
    Processing Record 31 of Set 12 | malanje
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=malanje
    Processing Record 32 of Set 12 | baiyin
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=baiyin
    Processing Record 33 of Set 12 | sinnamary
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=sinnamary
    Processing Record 34 of Set 12 | twentynine palms
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=twentynine palms
    Processing Record 35 of Set 12 | nelson bay
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=nelson bay
    Processing Record 36 of Set 12 | adrar
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=adrar
    Processing Record 37 of Set 12 | baie-comeau
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=baie-comeau
    Processing Record 38 of Set 12 | antalaha
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=antalaha
    Processing Record 39 of Set 12 | demba
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=demba
    Processing Record 40 of Set 12 | tucumcari
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=tucumcari
    Processing Record 41 of Set 12 | nagato
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=nagato
    Processing Record 42 of Set 12 | manama
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=manama
    Processing Record 43 of Set 12 | belmonte
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=belmonte
    Processing Record 44 of Set 12 | sudbury
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=sudbury
    Processing Record 45 of Set 12 | baykit
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=baykit
    Processing Record 46 of Set 12 | mersing
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=mersing
    Processing Record 47 of Set 12 | kondinskoye
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=kondinskoye
    Processing Record 48 of Set 12 | warri
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=warri
    Processing Record 49 of Set 12 | bali chak
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=bali chak
    Processing Record 0 of Set 13 | englewood
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=englewood
    Processing Record 1 of Set 13 | itainopolis
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=itainopolis
    City not found!
    Processing Record 2 of Set 13 | hoopstad
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=hoopstad
    Processing Record 3 of Set 13 | santo antonio do ica
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=santo antonio do ica
    Processing Record 4 of Set 13 | kahului
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=kahului
    Processing Record 5 of Set 13 | livaderon
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=livaderon
    City not found!
    Processing Record 6 of Set 13 | port hedland
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=port hedland
    Processing Record 7 of Set 13 | punta de piedra
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=punta de piedra
    Processing Record 8 of Set 13 | key west
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=key west
    Processing Record 9 of Set 13 | hutchinson
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=hutchinson
    Processing Record 10 of Set 13 | herat
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=herat
    Processing Record 11 of Set 13 | cape canaveral
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=cape canaveral
    Processing Record 12 of Set 13 | taraz
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=taraz
    Processing Record 13 of Set 13 | ilmajoki
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=ilmajoki
    Processing Record 14 of Set 13 | peniche
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=peniche
    Processing Record 15 of Set 13 | catio
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=catio
    Processing Record 16 of Set 13 | salmas
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=salmas
    Processing Record 17 of Set 13 | kang
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=kang
    Processing Record 18 of Set 13 | bundaberg
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=bundaberg
    Processing Record 19 of Set 13 | peleduy
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=peleduy
    Processing Record 20 of Set 13 | chuguyevka
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=chuguyevka
    Processing Record 21 of Set 13 | waiouru
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=waiouru
    Processing Record 22 of Set 13 | louisbourg
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=louisbourg
    City not found!
    Processing Record 23 of Set 13 | siddapur
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=siddapur
    Processing Record 24 of Set 13 | sherrelwood
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=sherrelwood
    Processing Record 25 of Set 13 | broome
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=broome
    Processing Record 26 of Set 13 | yerkoy
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=yerkoy
    Processing Record 27 of Set 13 | usinsk
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=usinsk
    Processing Record 28 of Set 13 | crab hill
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=crab hill
    City not found!
    Processing Record 29 of Set 13 | chokurdakh
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=chokurdakh
    Processing Record 30 of Set 13 | praya
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=praya
    Processing Record 31 of Set 13 | miri
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=miri
    Processing Record 32 of Set 13 | zuwarah
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=zuwarah
    Processing Record 33 of Set 13 | haifa
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=haifa
    Processing Record 34 of Set 13 | ubauro
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=ubauro
    Processing Record 35 of Set 13 | la trinidad
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=la trinidad
    Processing Record 36 of Set 13 | suining
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=suining
    Processing Record 37 of Set 13 | tupa
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=tupa
    City not found!
    Processing Record 38 of Set 13 | mogadishu
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=mogadishu
    Processing Record 39 of Set 13 | pisz
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=pisz
    Processing Record 40 of Set 13 | puerto ayacucho
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=puerto ayacucho
    Processing Record 41 of Set 13 | vila franca do campo
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=vila franca do campo
    Processing Record 42 of Set 13 | nantucket
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=nantucket
    Processing Record 43 of Set 13 | laguna
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=laguna
    Processing Record 44 of Set 13 | puquio
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=puquio
    Processing Record 45 of Set 13 | sorland
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=sorland
    Processing Record 46 of Set 13 | hunza
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=hunza
    City not found!
    Processing Record 47 of Set 13 | yar-sale
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=yar-sale
    Processing Record 48 of Set 13 | waingapu
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=waingapu
    Processing Record 49 of Set 13 | abu kamal
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=abu kamal
    Processing Record 0 of Set 14 | sabzevar
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=sabzevar
    Processing Record 1 of Set 14 | baruun-urt
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=baruun-urt
    Processing Record 2 of Set 14 | kathmandu
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=kathmandu
    Processing Record 3 of Set 14 | nuuk
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=nuuk
    Processing Record 4 of Set 14 | balabac
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=balabac
    Processing Record 5 of Set 14 | cumana
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=cumana
    Processing Record 6 of Set 14 | gwadar
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=gwadar
    Processing Record 7 of Set 14 | gazanjyk
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=gazanjyk
    Processing Record 8 of Set 14 | ust-omchug
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=ust-omchug
    Processing Record 9 of Set 14 | ubatuba
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=ubatuba
    Processing Record 10 of Set 14 | hobbs
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=hobbs
    Processing Record 11 of Set 14 | ponta do sol
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=ponta do sol
    Processing Record 12 of Set 14 | candido mendes
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=candido mendes
    Processing Record 13 of Set 14 | tarija
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=tarija
    Processing Record 14 of Set 14 | baneh
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=baneh
    Processing Record 15 of Set 14 | waipawa
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=waipawa
    Processing Record 16 of Set 14 | vung tau
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=vung tau
    Processing Record 17 of Set 14 | moree
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=moree
    Processing Record 18 of Set 14 | ovalle
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=ovalle
    Processing Record 19 of Set 14 | rio pardo
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=rio pardo
    Processing Record 20 of Set 14 | viedma
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=viedma
    Processing Record 21 of Set 14 | we
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=we
    City not found!
    Processing Record 22 of Set 14 | naryan-mar
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=naryan-mar
    Processing Record 23 of Set 14 | cochrane
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=cochrane
    Processing Record 24 of Set 14 | yarada
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=yarada
    Processing Record 25 of Set 14 | xuanzhou
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=xuanzhou
    Processing Record 26 of Set 14 | praia
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=praia
    Processing Record 27 of Set 14 | barsovo
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=barsovo
    Processing Record 28 of Set 14 | namatanai
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=namatanai
    Processing Record 29 of Set 14 | karaul
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=karaul
    City not found!
    Processing Record 30 of Set 14 | samalaeulu
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=samalaeulu
    City not found!
    Processing Record 31 of Set 14 | bairiki
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=bairiki
    City not found!
    Processing Record 32 of Set 14 | jimo
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=jimo
    Processing Record 33 of Set 14 | negombo
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=negombo
    Processing Record 34 of Set 14 | semypolky
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=semypolky
    Processing Record 35 of Set 14 | grand-lahou
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=grand-lahou
    Processing Record 36 of Set 14 | pangody
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=pangody
    Processing Record 37 of Set 14 | shenjiamen
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=shenjiamen
    Processing Record 38 of Set 14 | boyolangu
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=boyolangu
    Processing Record 39 of Set 14 | candelaria
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=candelaria
    Processing Record 40 of Set 14 | ahuimanu
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=ahuimanu
    Processing Record 41 of Set 14 | willowmore
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=willowmore
    Processing Record 42 of Set 14 | limoges
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=limoges
    Processing Record 43 of Set 14 | tanout
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=tanout
    Processing Record 44 of Set 14 | kuytun
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=kuytun
    Processing Record 45 of Set 14 | libourne
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=libourne
    Processing Record 46 of Set 14 | kaeo
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=kaeo
    Processing Record 47 of Set 14 | port charlotte
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=port charlotte
    Processing Record 48 of Set 14 | zheleznodorozhnyy
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=zheleznodorozhnyy
    Processing Record 49 of Set 14 | gombong
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=gombong
    Processing Record 0 of Set 15 | te anau
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=te anau
    Processing Record 1 of Set 15 | vabalninkas
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=vabalninkas
    Processing Record 2 of Set 15 | puerto penasco
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=puerto penasco
    Processing Record 3 of Set 15 | kuyanovo
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=kuyanovo
    Processing Record 4 of Set 15 | sisimiut
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=sisimiut
    Processing Record 5 of Set 15 | kazalinsk
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=kazalinsk
    City not found!
    Processing Record 6 of Set 15 | szubin
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=szubin
    Processing Record 7 of Set 15 | natal
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=natal
    Processing Record 8 of Set 15 | astoria
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=astoria
    Processing Record 9 of Set 15 | patiya
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=patiya
    Processing Record 10 of Set 15 | sri aman
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=sri aman
    Processing Record 11 of Set 15 | villaviciosa
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=villaviciosa
    Processing Record 12 of Set 15 | menongue
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=menongue
    Processing Record 13 of Set 15 | puerto escondido
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=puerto escondido
    Processing Record 14 of Set 15 | hervey bay
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=hervey bay
    Processing Record 15 of Set 15 | raga
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=raga
    City not found!
    Processing Record 16 of Set 15 | rock springs
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=rock springs
    Processing Record 17 of Set 15 | ust-ilimsk
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=ust-ilimsk
    Processing Record 18 of Set 15 | esfarayen
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=esfarayen
    Processing Record 19 of Set 15 | high rock
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=high rock
    Processing Record 20 of Set 15 | purranque
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=purranque
    Processing Record 21 of Set 15 | safwah
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=safwah
    City not found!
    Processing Record 22 of Set 15 | kamojima
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=kamojima
    Processing Record 23 of Set 15 | tilichiki
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=tilichiki
    Processing Record 24 of Set 15 | kismayo
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=kismayo
    City not found!
    Processing Record 25 of Set 15 | maragogi
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=maragogi
    Processing Record 26 of Set 15 | jiuquan
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=jiuquan
    Processing Record 27 of Set 15 | boende
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=boende
    Processing Record 28 of Set 15 | tabou
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=tabou
    Processing Record 29 of Set 15 | chemal
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=chemal
    Processing Record 30 of Set 15 | kasongo-lunda
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=kasongo-lunda
    Processing Record 31 of Set 15 | rafaela
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=rafaela
    Processing Record 32 of Set 15 | the pas
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=the pas
    Processing Record 33 of Set 15 | larsnes
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=larsnes
    Processing Record 34 of Set 15 | vestmannaeyjar
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=vestmannaeyjar
    Processing Record 35 of Set 15 | odawara
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=odawara
    Processing Record 36 of Set 15 | opuwo
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=opuwo
    Processing Record 37 of Set 15 | lamar
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=lamar
    Processing Record 38 of Set 15 | margate
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=margate
    Processing Record 39 of Set 15 | atambua
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=atambua
    Processing Record 40 of Set 15 | limpapa
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=ac5bb07823787a1e759cb6180b71b6dc&q=limpapa
    


```python
#create data frame
city_data_pd = pd.DataFrame(city_data)

lats = city_data_pd["Lat"]
max_temps = city_data_pd["Max Temp"]
humidity = city_data_pd["Humidity"]
cloudiness = city_data_pd["Cloudiness"]
wind_speed = city_data_pd["Wind Speed"]

city_data_pd.to_csv("output_data/cities.csv", index_label="City_ID")

```


```python
#Temperature (F) vs. Latitude
plt.scatter(lats,
            max_temps,
            color="red",
            edgecolor="black",
            linewidths=1,
            marker="o",
            alpha=0.8,
            label="Cities")

plt.title("Temperature (F) vs. Latitude")
plt.ylabel("Temperature (F)")
plt.xlabel("Latitude")
plt.grid(True)

plt.savefig("output_data/Temperature.png")

plt.show()

```


![png](output_4_0.png)



```python
#Humidity (%) vs. Latitude
plt.scatter(lats,
            humidity,
            color="blue",
            edgecolor="black", 
            linewidths=1, 
            marker="o", 
            alpha = 0.8,
            label="Cities")

plt.title("Humidity (%) vs. Latitude")
plt.ylabel("Humidity (%)")
plt.xlabel("Latitude")
plt.grid(True)

plt.savefig("output_data/Humidity.png")

plt.tight_layout()
plt.show()
```


![png](output_5_0.png)



```python
#Cloudiness (%) vs. Latitude
plt.scatter(lats,
            cloudiness,
            color="grey", 
            edgecolor="black", 
            linewidths=1, 
            marker="o", 
            alpha = 0.8,
            label="Cities")

plt.title("#Cloudiness (%) vs. Latitude")
plt.ylabel("Cloudiness (%)")
plt.xlabel("Latitude")
plt.grid(True)

plt.savefig("output_data/Cloudiness.png")

plt.tight_layout()
plt.show()
```


![png](output_6_0.png)



```python
#Wind Speed (mph) vs. Latitude
plt.scatter(lats,
            wind_speed,
            color="green",
            edgecolor="black",
            linewidths=1,
            marker="o",
            alpha=0.8,
            label="Cities")

plt.title("Wind Speed (mph) vs. Latitude")
plt.ylabel("Wind Speed (mph)")
plt.xlabel("Latitude")
plt.grid(True)

plt.savefig("output_data/Wind.png")

plt.tight_layout()
plt.show()

```


![png](output_7_0.png)

