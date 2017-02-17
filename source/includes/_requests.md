# Requests 

## Create and send a request 

```shell
curl -X POST -H "Authorization: <AUTHORIZATION_TOKEN>" -H "Content-Type: application/json" -d '{
    "karma": 10,
    "location": {
        "lat": 33.7490,
        "lon": -84.3884
    },
    "message": "How are you doing today?",
    "override": false,
    "rating": 5,
    "type": "image"
}' "https://node.ucic.vc/api/v04/requests"
```

```javascript
```

> The above command returns JSON structured like this:

```json
{
  "ReportedText": null,
  "RI": "46985",
  "Address": "214 Capitol Pl SW, Atlanta, GA 30303, USA",
  "City": "Atlanta",
  "Competes": 0,
  "CountryCode": "US",
  "CreatorUI": 611,
  "End": "2017-01-05T17:44:16.603Z",
  "Karma": 10,
  "Lat": 33.749,
  "Lon": -84.3884,
  "Message": "How are you doing today?",
  "Rating": 5,
  "Start": "2017-01-03T17:44:16.603Z",
  "Street": "214, Capitol Place Southwest",
  "Type": 0,
  "Vulgar": false,
  "Reported": null,
  "Country": "United States"
}
```

This endpoint creates and sends a request.

### HTTP Request

POST https://node.ucic.vc/api/v04/requests

### Query Parameters

Parameter | Type | Description
--------- | ---- | -----------
karma | Unsigned Integer | Karma to be awarded for this request. Default is 10
location | { lat, lon } | location lat lon request coordinates
message | String | Request message content body
override | Boolean | Override time of day exception and send request anyway
rating | Unsigned Integer | Default request rating (unused). Default is 5
type | String | Type of request.  'image' for image or 'video' for video
receivers | [ Unsigned Integer ] | (Optional) List of receiver user IDs

### Errors
Error | Meaning
---------- | -------
400 | MAX_ACTIVE_REQUESTS_EXCEEDED -- You have too many active requests pending
400 | REQUIRED_FIELD_MISSING -- You are missing required fields location, message, or type
400 | REQUEST_OUTSIDE_PERMITTED_TIME -- Your request is outside the hours of 07 - 22 in the local time

## Update a user's request's seen status

```shell
curl -X PUT -H "Authorization: <AUTHORIZATION_TOKEN>" -H "Content-Type: application/json" -d '{ "seen": true }' "https://node.ucic.vc/api/v04/requests/31832" 
```

```javascript
```

> The above command returns 204 on success:

This endpoint update's the current user's request's status.

### HTTP Request

`PUT https://node.ucic.vc/api/v04/requests/<ID>`

### Body Parameters

Parameter | Type | Description
--------- | ---- | -----------
seen | Boolean | Seen status of request 

