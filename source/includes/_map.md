# Map 

## Get Map Markers and Clusters

```shell
curl -X GET -H "Authorization: <AUTHORIZATION_TOKEN>" "https://node.ucic.vc/api/v04/map/?north=72.57706249077567&south=-72.57707684644146&east=72.32144437730312&west=-72.32142057269812&zoom=2"
```

```javascript

```

> The above command returns JSON structured like this:

```json
{
  "markers": [{   // note: only sent if layer is "user" (or missing)
    "id": "39293",
    "lat": 31.6659954,
    "logo": "http://staging-media.ucic.vc/media/58FBBD39-8172-4271-A9B0-8ED4E27A79D0/micro.jpg",
    "lon": -6.9485274,
    "subtitle": "",
    "timeZoneMinutes": -300,
    "title": "Khan Jan",
    "type": "user"
  }],
  "requests": [{   // note: only sent if layer is "request"
      "id": "300038",
      "questionId": "8285A6A7-BF41-4EE5-BDDE-4C7377FC68ED",
      "lat": 45.3735,
      "lon": -84.8978,
      "message": "What's happening over there?",
      "start": "2017-04-06T19:43:39.000Z",
      "end": "2017-04-13T19:43:39.000Z",
      "radius": 7829.24,
      "responseCount": 2,
      "discoverResponses": [{  // up to 10 entries in array
        "type": 0,
        "badge": "https://media.ucic.vc/assets/tags/CA.png",
        "caption": "some text that's part of the response",
      	"cardId": "F3A0F6F1-E61B-43E0-B78E-9309E0E60A55",
        "media": "https://media.ucic.vc/media/F3A0F6F1-E61B-43E0-B78E-9309E0E60A55/thumb.jpg",
        "displayMedia": "https://media.ucic.vc/media/F3A0F6F1-E61B-43E0-B78E-9309E0E60A55/display.jpg"
      }],
      "creator": {
        "userAvatar": "https://media.ucic.vc/media/ADBDACEB-5D03-470C-89F5-C01C29BD8A89/thumb.jpg",
        "userId": 195685,
        "userName": "Khan"
      },
      "followers": [{
        "userId": 12345,
        "userName": "Carl Sagan",
        "userAvatar": "https://media.ucic.vc/media/ADBDACEB-5D03-470C-89F5-C01C29BD8A89/thumb.jpg"
      }]
    }],
  "clusters": [
    {
      "lat": 46.09142816319215,
      "lon": 26.981662140000008,
      "count": 5
    },
    {
      "lat": 10.0620643242315,
      "lon": -84.5892040031087,
      "count": 6
    },
    {
      "lat": 43.029565867868484,
      "lon": -79.93623185692996,
      "count": 45
    }
  ]
}
```

This endpoint retrieves markers and clusters on the map. It supports a *layer* query parameter to specify which data type to display on the map. If not provided, it defaults to the "user" layer.

### HTTP Request

`GET https://node.ucic.vc/api/v04/map`

### Query Parameters

| Parameter | Type             | Description                              |
| --------- | ---------------- | ---------------------------------------- |
| north     | Decimal (38)     | Northern latitude boundary of bounding box.  Max: 90, Min: 90 |
| south     | Decimal (38)     | Southern latitude boundary of bounding box.  Max: 90, Min: -90 |
| east      | Decimal (38)     | Eastern longitude boundary of bounding box.  Max: 180, Min: -180 |
| west      | Decimal (38)     | Western longitude boundary of bounding box. Max: 180, Min: -180 |
| zoom      | Unsigned Integer | Google Maps Zoom Level to retrieve results at.  Min: 0, Max: 11 |
| layer     | String           | Specify the request map data layer. Current supported values are "request" and "user" (default) |

## Get Map Event layer

```shell
curl -X GET -H "Authorization: <AUTHORIZATION_TOKEN>" "https://node.ucic.vc/api/v04/map/?north=72.57706249077567&south=-72.57707684644146&east=72.32144437730312&west=-72.32142057269812&zoom=2&layer=events&categories=sports,festivals"
```

```javascript

```

> The above command returns JSON structured like this:

```json
[{
  "id": "02b6qM8epkmW",
  "title": "Montana Avenue ART WALK",
  "description": "Join us for a family/friends/date night of art, music, treats & shopping on 11th blocks of the scenic Montana Avenue. View many local and famed artists, sample the treats and dine in USA Today's top restaurant pics. 6th - 17th street.",
  "categoryId": "festivals",
  "scope": "locality",
  "country": "US",
  "location": {
    "lat": 34.0345,
    "lon": -118.492
  },
  "radius": 1500,
  "mediaCount": 99,
  "rank": 69,
  "start": "2017-07-21T00:00:00.000Z",
  "end": "2017-07-21T04:00:00.000Z",
  "updated": "2017-07-13T07:29:03.000Z"
}]
```

This endpoint retrieves event markers for the map. This layer does not do any clustering, instead the events returned are filtered based on the zoom level provided in the query parameters such that higher "rank" events appear at lower zoom levels (higher altitudes). 

Note: many of the events are submitted by users of the Predict HQ api and as such, the reliability of the data in each field should be taken with a grain of salt; start/end times may not be completely accurate, rank may be overstated, description may be missing, etc.

**Note:** Radius expressed in meters.

### HTTP Request

`GET https://node.ucic.vc/api/v04/map?layer=events&categories=sports,festivals,expos,severe-weather&north=72.577&south=68.584&east=72.321&west=69.765&zoom=3`

### Query Parameters

| Parameter  | Type              | Description                              |
| ---------- | ----------------- | ---------------------------------------- |
| north      | Decimal (38)      | Northern latitude boundary of bounding box.  Max: 90, Min: 90 |
| south      | Decimal (38)      | Southern latitude boundary of bounding box.  Max: 90, Min: -90 |
| east       | Decimal (38)      | Eastern longitude boundary of bounding box.  Max: 180, Min: -180 |
| west       | Decimal (38)      | Western longitude boundary of bounding box. Max: 180, Min: -180 |
| zoom       | float             | Map zoom level to retrieve results at.  Min: 0, Max: 20. Determines what events are returned |
| layer      | String ('events') | (Required) specifies the event map layer is the one to return. If omitted, will return the default (user) map layer |
| categories | String            | A comma-seperated list of event category IDs to return. Use the GET /map/eventCategories route below to retrive the list of supported event categories. Example usage in query url: `&categories=sports,culture,shows` |

## Get Event Map Layer Categories

```shell
curl -X GET -H "Authorization: <AUTHORIZATION_TOKEN>" "https://node.ucic.vc/api/v04/map/eventCategories"
```

```javascript

```

> The above command returns JSON structured like this:

```json
[{
  "name": "Concerts & Shows",
  "icon": "https://s3-us-west-2.amazonaws.com/ucic-production/assets/events/shows.png",
  "categoryId": "shows",
  "eventCount": 941
},{
  "name": "Conferences & Expos",
  "icon": "https://s3-us-west-2.amazonaws.com/ucic-production/assets/events/expos.png",
  "categoryId": "expos",
  "eventCount": 185
}]
```

This endpoint provides the available categories and their associated info for use with the events map layer. When querying the events map layer, use the values provided as the `categoryId` for each category to include those events in the returned data.


### HTTP Request

`GET https://node.ucic.vc/api/v04/map/eventCategories`
