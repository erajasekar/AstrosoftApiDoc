---
title: Astrosoft API Reference

language_tabs: # must be one of https://git.io/vQNgJ
  - shell
  - javascript

toc_footers:
  - <a href='https://www.innovativeastrosolutions.com/'>Sign Up for a Developer Key</a>
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

> Make sure to replace `your_api_key` with your API key.

Astrosoft uses API key in request header to authenticate clients. You can request new API key at our [website](https://www.innovativeastrosolutions.com/).

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
curl --request POST \
  --url https://api.innovativeastrosolutions.com/v0/horoscope \
  --header 'content-type: application/json' \
  --header 'x-api-key: your_api_key' \
  --data '{\n    "name": "Your Name",\n    "place": {\n        "name": "Sydney, AU",\n        "longitude": 151.209296,\n        "latitude": -33.868820,\n        "timeZoneId": "Australia/Sydney"\n    },\n    "year": 1967,\n    "month": 02,\n    "date": 26,\n    "hour": 0,\n    "minutes": 1,\n    "seconds": 0,\n    "options": {\n        "Ayanamsa": "LAHARI"\n    }\n}'
```

```javascript
var data = "{\n    \"name\": \"Your Name\",\n    \"place\": {\n        \"name\": \"Sydney, AU\",\n        \"longitude\": 151.209296,\n        \"latitude\": -33.868820,\n        \"timeZoneId\": \"Australia/Sydney\"\n    },\n    \"year\": 1967,\n    \"month\": 02,\n    \"date\": 26,\n    \"hour\": 0,\n    \"minutes\": 1,\n    \"seconds\": 0,\n    \"options\": {\n        \"Ayanamsa\": \"LAHARI\"\n    }\n}";

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

> The above requests returns JSON response like this:

```json
{
    "planetaryInfo": {
        "Sun": {
            "planet": "Sun",
            "nakshathraPada": {
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
            "nakshathraPada": {
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
            "nakshathraPada": {
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
            "nakshathraPada": {
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
            "nakshathraPada": {
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
            "nakshathraPada": {
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
            "nakshathraPada": {
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
            "nakshathraPada": {
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
            "nakshathraPada": {
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
            "nakshathraPada": {
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


