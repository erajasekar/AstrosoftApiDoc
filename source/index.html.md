---
title: Astrosoft API Reference

language_tabs: # must be one of 
  - csharp
  - shell
  - javascript

toc_footers:
  - By <a href='https://www.innovativeastrosolutions.com/'>innovativeastrosolutions.com</a>
  - <a href='https://github.com/lord/slate'>Documentation Powered by Slate</a>

includes:
  - response_codes

search: true
---

# Introduction

Welcome to Astrosoft API! You can use our API to generate vedic astrology reports by providing birth data.

You can view code examples in the right hand side, and you can switch the programming language of the examples with the tabs in the top right.

# Authentication

> To authorize, provide `x-api-key` in the request header:

```shell
# With shell, you can just pass the correct header with each request
curl "https://api.innovativeastrosolutions.com/v0/horoscope"
  -H "x-api-key: your_api_key"
```

```javascript
var xhr = new XMLHttpRequest();
xhr.withCredentials = true;
xhr.open("POST", "https://api.innovativeastrosolutions.com/v0/horoscope");
xhr.setRequestHeader("x-api-key", "your_api_key");
```

```csharp
var client = new RestClient("https://api.innovativeastrosolutions.com/v0/panchang");
var request = new RestRequest(Method.POST);
request.AddHeader("content-type", "application/json");
request.AddHeader("x-api-key", "your_api_key");
```

> Make sure to replace `your_api_key` with your API key.

Astrosoft uses API key in request header to authenticate clients. You can request new API key by contacting us at innovativeastrosolutions@gmail.com.

<aside class="notice">
You must replace <code>your_api_key</code> with your personal API key.
</aside>

# Documentation

## Request JSON Parameters

> Request JSON should provide birth data in following JSON format

```json
{
    "name": "Your Name",
    "place": {
        "name": "Sydney, AU",
        "longitude": 151.209296,
        "latitude": -33.868820,
        "timeZoneId": "Australia/Sydney"
    },
    "year": 1967,
    "month": 02,
    "date": 26,
    "hour": 0,
    "minutes": 1,
    "seconds": 0,
    "options": {
        "Ayanamsa": "LAHARI"
    }
}
```

POST requests expects following birth information in Request body in JSON format.

| Parameter        | Data type   | Description                              |
| ---------------- | ----------- | ---------------------------------------- |
| name             | String      | Person Name                              |
| place            | JSON Object | Birth Place. ( See below `place.*` params ) |
| place.name       | String      | Place Name                               |
| place.longitude  | Double      | Longitude ( Eg: `151.20` )               |
| place.latitude   | Double      | Latitude ( Eg: `-33.86` )                |
| place.timeZoneId | String      | Timezone Id ( Eg:  ` Australia/Sydney` ) |
| year             | Int         | Year ( Eg: `2017` )                      |
| month            | Int         | Month ( Eg: `12` )                       |
| date             | Int         | Date ( Eg: `31` )                        |
| hour             | Int         | Hour in 24 hour format ( Eg: `23` )      |
| minutes          | Int         | Minutes ( Eg: `10` )                     |
| seconds          | Int         | Seconds ( Eg: `00`)                      |
| options          | JSON Object | Addtional Options. ( See below `options.*` params ) |
| options.Ayanamsa | String      | Ayanamsa to use. (  Supported values are `LAHARI` , `RAMAN`, `KRISHNAMURTHI` ) |

* You can use this [online tool](https://www.latlong.net/) to find latitude & longitude of the place.
* You can look up valid TimezoneIds from this [wiki page](https://en.wikipedia.org/wiki/List_of_tz_database_time_zones)

<aside class="notice">
To make this easier, we will soon provide an API that will return latitude, longitude and TimezoneId for given first few letters for city.
</aside>

## Horoscope Details

This endpoint returns Horscope details for birth data provided in Request Body.

### HTTP Request

`POST https://api.innovativeastrosolutions.com/v0/horoscope`

```shell
curl -X POST \
  https://api.innovativeastrosolutions.com/v0/horoscope \
  -H 'content-type: application/json' \
  -H 'x-api-key: your_api_key' \
  -d '{
    "name": "Your Name",
    "place": {
        "name": "Sydney, AU",
        "longitude": 151.209296,
        "latitude": -33.868820,
        "timeZoneId": "Australia/Sydney"
    },
    "year": 1967,
    "month": 02,
    "date": 26,
    "hour": 0,
    "minutes": 1,
    "seconds": 0,
    "options": {
        "Ayanamsa": "LAHARI"
    }
}'
```

```javascript
var data = JSON.stringify({
    "name": "Your Name",
    "place": {
        "name": "Sydney, AU",
        "longitude": 151.209296,
        "latitude": -33.868820,
        "timeZoneId": "Australia/Sydney"
    },
    "year": 1967,
    "month": 02,
    "date": 26,
    "hour": 0,
    "minutes": 1,
    "seconds": 0,
    "options": {
        "Ayanamsa": "LAHARI"
    }
});
var xhr = new XMLHttpRequest();
xhr.withCredentials = true;

xhr.addEventListener("readystatechange", function () {
  if (this.readyState === 4) {
    console.log(this.responseText);
  }
});

xhr.open("POST", "https://api.innovativeastrosolutions.com/v0/horoscope");
xhr.setRequestHeader("x-api-key", "your_api_key");
xhr.setRequestHeader("content-type", "application/json");

xhr.send(data);
```

```csharp
var client = new RestClient("https://api.innovativeastrosolutions.com/v0/horoscope");
var request = new RestRequest(Method.POST);
request.AddHeader("content-type", "application/json");
request.AddHeader("x-api-key", "your_api_key");
request.AddParameter("application/json", "{\n    \"name\": \"Your Name\",\n    \"place\": {\n        \"name\": \"Sydney, AU\",\n        \"longitude\": 151.209296,\n        \"latitude\": -33.868820,\n        \"timeZoneId\": \"Australia/Sydney\"\n    },\n    \"year\": 1967,\n    \"month\": 02,\n    \"date\": 26,\n    \"hour\": 0,\n    \"minutes\": 1,\n    \"seconds\": 0,\n    \"options\": {\n        \"Ayanamsa\": \"LAHARI\"\n    }\n}", ParameterType.RequestBody);
IRestResponse response = client.Execute(request);
```

> The above requests returns Horoscope JSON response like this:

```json
{
    "planetaryInfo": {
        "Sun": {
            "planet": "Sun",
            "nakshatraPada": {
                "nak": "Shatabhisha",
                "pada": 2
            },
            "position": 312.8804768178875,
            "sign": "Aquarius",
            "signPosition": 12.880476817887484,
            "retro": false
        },
        "Moon": {
            "planet": "Moon",
            "nakshatraPada": {
                "nak": "Purva Phalguni",
                "pada": 4
            },
            "position": 144.81099408451155,
            "sign": "Leo",
            "signPosition": 24.81099408451155,
            "retro": false
        },
        "Mars": {
            "planet": "Mars",
            "nakshatraPada": {
                "nak": "Swathi",
                "pada": 1
            },
            "position": 189.07028979479819,
            "sign": "Libra",
            "signPosition": 9.070289794798185,
            "retro": false
        },
        "Mercury": {
            "planet": "Mercury",
            "nakshatraPada": {
                "nak": "Purva Bhadrapada",
                "pada": 2
            },
            "position": 324.9373992941768,
            "sign": "Aquarius",
            "signPosition": 24.937399294176828,
            "retro": true
        },
        "Jupiter": {
            "planet": "Jupiter",
            "nakshatraPada": {
                "nak": "Punarvasu",
                "pada": 4
            },
            "position": 91.93852678494463,
            "sign": "Cancer",
            "signPosition": 1.938526784944628,
            "retro": true
        },
        "Venus": {
            "planet": "Venus",
            "nakshatraPada": {
                "nak": "Uttra Bhadrapada",
                "pada": 2
            },
            "position": 338.63741979962236,
            "sign": "Pisces",
            "signPosition": 8.637419799622364,
            "retro": false
        },
        "Saturn": {
            "planet": "Saturn",
            "nakshatraPada": {
                "nak": "Uttra Bhadrapada",
                "pada": 1
            },
            "position": 335.8497349411362,
            "sign": "Pisces",
            "signPosition": 5.849734941136205,
            "retro": false
        },
        "Rahu": {
            "planet": "Rahu",
            "nakshatraPada": {
                "nak": "Bharani",
                "pada": 1
            },
            "position": 15.49245914997472,
            "sign": "Aries",
            "signPosition": 15.49245914997472,
            "retro": false
        },
        "Ketu": {
            "planet": "Ketu",
            "nakshatraPada": {
                "nak": "Swathi",
                "pada": 3
            },
            "position": 195.4924591499747,
            "sign": "Libra",
            "signPosition": 15.492459149974707,
            "retro": false
        },
        "Ascendant": {
            "planet": "Ascendant",
            "nakshatraPada": {
                "nak": "Moola",
                "pada": 1
            },
            "position": 240.17358459540253,
            "sign": "Sagittarius",
            "signPosition": 0.1735845954025308,
            "retro": false
        }
    }
}
```

## Panchang Details

This endpoint returns Panchang details for time and place data provided in Request Body.

### HTTP Request

`POST https://api.innovativeastrosolutions.com/v0/panchang`


```shell
curl -X POST \
  https://api.innovativeastrosolutions.com/v0/panchang \
  -H 'content-type: application/json' \
  -H 'x-api-key: your_api_key' \
  -d '{
    "name": "Panchang",
    "place": {
        "name": "Tampa",
        "longitude": -82.45843,
        "latitude": 27.94752,
        "timeZoneId": "America/New_York"
    },
    "year": 2017,
    "month": 10,
    "date": 14,
    "hour": 6,
    "minutes": 0,
    "seconds": 0,
    "options": {
        "Ayanamsa": "LAHARI"
    }
}'
```

```javascript
var data = JSON.stringify({
  "name": "Panchang",
  "place": {
    "name": "Tampa",
    "longitude": -82.45843,
    "latitude": 27.94752,
    "timeZoneId": "America/New_York"
  },
  "year": 2017,
  "month": 10,
  "date": 14,
  "hour": 6,
  "minutes": 0,
  "seconds": 0,
  "options": {
    "Ayanamsa": "LAHARI"
  }
});

var xhr = new XMLHttpRequest();
xhr.withCredentials = true;

xhr.addEventListener("readystatechange", function () {
  if (this.readyState === 4) {
    console.log(this.responseText);
  }
});

xhr.open("POST", "https://api.innovativeastrosolutions.com/v0/panchang");
xhr.setRequestHeader("x-api-key", "your_api_key");
xhr.setRequestHeader("content-type", "application/json");

xhr.send(data);
```

```csharp
var client = new RestClient("https://api.innovativeastrosolutions.com/v0/panchang");
var request = new RestRequest(Method.POST);
request.AddHeader("content-type", "application/json");
request.AddHeader("x-api-key", "your_api_key");
request.AddParameter("application/json", "{\n    \"name\": \"Panchang\",\n    \"place\": {\n        \"name\": \"Tampa\",\n        \"longitude\": -82.45843,\n        \"latitude\": 27.94752,\n        \"timeZoneId\": \"America/New_York\"\n    },\n    \"year\": 2017,\n    \"month\": 10,\n    \"date\": 14,\n    \"hour\": 6,\n    \"minutes\": 0,\n    \"seconds\": 0,\n    \"options\": {\n        \"Ayanamsa\": \"LAHARI\"\n    }\n}", ParameterType.RequestBody);
IRestResponse response = client.Execute(request);
```

> The above request returns Panchang Response JSON like this

```json
{
    "time": "06:00 AM",
    "date": "Oct 14 2017",
    "weekday": "Saturday",
    "timeZoneId": "America/New_York",
    "sunrise": "07:29 AM",
    "sunset": "07:01 PM",
    "nakshatra": {
        "name": "Ashlesha",
        "endTime": "20:50"
    },
    "thithi": {
        "name": "Dasami",
        "endTime": "16:33"
    },
    "yoga": {
        "name": "Sadhya",
        "endTime": "13:33"
    },
    "karna": {
        "first": {
            "name": "Visti",
            "endTime": "16:33"
        },
        "second": {
            "name": "Bava",
            "endTime": "28:01"
        }
    },
    "paksha": "Krishna",
    "rahuKala": "09:00 AM - 10:30 AM",
    "yamaKanda": "01:30 PM - 03:00 PM",
    "auspiciousTime": [
        "07.00 - 07.30 am , 10.30 - 12.00 pm",
        "12.00 - 01.00 pm , 05.00 - 06.00 pm",
        "06.00 - 07.30 pm , 09.00 - 10.00 pm"
    ]
}
```
