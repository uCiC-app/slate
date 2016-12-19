# Map 

## Get markers and clusters on the map

```shell
curl -X GET -H "Authorization: 007C9B0A-B92B-4D0F-9561-2E2BA932FE71" -H "Cache-Control: no-cache" -H "Postman-Token: f1fd867f-66b7-d917-f20b-94b4ae59ac25" "https://node.ucic.vc/api/v04/map/?north=72.57706249077567&south=-72.57707684644146&east=72.32144437730312&west=-72.32142057269812&zoom=2"
curl "https://node.ucic.vc/api/v04/map/?north=72.57706249077567&south=-72.577076    84644146&east=72.32144437730312&west=-72.32142057269812&zoom=2"
  -H "Authorization: <AUTHORIZATION_TOKEN>"
```

```javascript
```

> The above command returns JSON structured like this:

```json
{
  "markers": [],
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

Parameter | Type | Description
--------- | ---- | -----------
north | Decimal (38) | Northern latitude boundary of bounding box.  Max: 90, Min: 90
south | Decimal (38) | Southern latitude boundary of bounding box.  Max: 90, Min: -90
east | Decimal (38) | Eastern longitude boundary of bounding box.  Max: 180, Min: -180
west | Decimal (38) | Western longitude boundary of bounding box. Max: 180, Min: -180
zoom | Unsigned Integer | Google Maps Zoom Level to retrieve results at.  Min 0:, Max: 11

