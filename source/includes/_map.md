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
  "markers": [{
    "id": "39293",
    "lat": 31.6659954,
    "logo": "http://staging-media.ucic.vc/media/58FBBD39-8172-4271-A9B0-8ED4E27A79D0/micro.jpg",
    "lon": -6.9485274,
    "subtitle": "",
    "timeZoneMinutes": -300,
    "title": "Khan Jan",
    "type": "user"
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

This endpoint retrieves markers and clusters on the map.

### HTTP Request

`GET https://node.ucic.vc/api/v04/map`

### Query Parameters

| Parameter | Type             | Description                              |
| --------- | ---------------- | ---------------------------------------- |
| north     | Decimal (38)     | Northern latitude boundary of bounding box.  Max: 90, Min: 90 |
| south     | Decimal (38)     | Southern latitude boundary of bounding box.  Max: 90, Min: -90 |
| east      | Decimal (38)     | Eastern longitude boundary of bounding box.  Max: 180, Min: -180 |
| west      | Decimal (38)     | Western longitude boundary of bounding box. Max: 180, Min: -180 |
| zoom      | Unsigned Integer | Google Maps Zoom Level to retrieve results at.  Min 0:, Max: 11 |

