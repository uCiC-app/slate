# Requests 

## Create and send a request 

```shell
curl -X POST -H "Authorization: <AUTHORIZATION_TOKEN>" -H "Content-Type: application/json" -d '{
    "location": {
        "lat": 33.7490,
        "lon": -84.3884,
        "radius": 750
    },
    "message": "How are you doing today?",
    "override": false,
    "requestType": 1
}' "https://node.ucic.vc/api/v04/requests"
```

```javascript

```

> The above command returns a 201 success code along with a json response like:

```json
{ 
	"Code": 0,
	"Message": ""
}
```
> In the event of an error, the response will be structured as:

```json
{ 
	"error": "ERROR_CODE"
}
```

This endpoint creates and sends a request.

### HTTP Request

POST https://node.ucic.vc/api/v04/requests

### Body Parameters

| Parameter    | Type                 | Description                              |
| ------------ | -------------------- | ---------------------------------------- |
| location\*   | { lat, lon, radius } | (Optional if receiverUI is provided) location request lat lon coordinates and radius(m). |
| message      | String               | Request message content body             |
| override     | Boolean              | (Optional, default: false) Override time of day exception and send request anyway |
| receiverUI\* | Unsigned Integer     | (Optional if location is provided) List of receiver user IDs |

\* **Note:** one of *location* or *receiverUI* must be provided which dictates whether this request will be a map request or direct request, respectively. If both are provided, the location will be ignored.

### Errors
| Error | Meaning                                  |
| ----- | ---------------------------------------- |
| 400   | MAX_ACTIVE_REQUESTS_EXCEEDED -- You have too many active requests pending |
| 400   | REQUIRED_FIELD_MISSING -- You are missing required fields location, message, or type |

## Get Nearby Requests

```shell
curl -X GET -H "Authorization: <AUTHORIZATION_TOKEN>" -H "Content-Type: application/json" "https://node.ucic.vc/api/v04/requests/nearest?lat=33.7490&lon=-84.3884"
```
```javascript

```

> The above command returns a 200 success code along with a json response like:

```json
[{ 
	"requestId": 51239,
	"message": "Can you show me what's happening there?",
	"start": "2017-03-28T18:45:33.286Z",
    "end": "2017-04-04T18:45:33.286Z",
	"requestType": 0,
    "responseCount": 1,
    "seen": false,
	"location": {
      "lat": 33.7490,
      "lon": -84.3884,
      "radius": 525
	},
    "discoverResponses": [{  // up to 3 entries in this array
        "type": 0,
        "badge": "https://media.ucic.vc/assets/tags/CA.png",
      	"cardId": "F3A0F6F1-E61B-43E0-B78E-9309E0E60A55",
        "media": "https://media.ucic.vc/media/F3A0F6F1-E61B-43E0-B78E-9309E0E60A55/thumb.jpg"
    }],
	"creator": {
      "userId": 39266,
      "userName": "Billy Jean",
      "userAvatar": "http://staging-media.ucic.vc/media/B94667C1-19A6-4973-9003-9723A36BBF0F/thumb.jpg"
	}
}, ...]
```

Retrieve the map requests that the provided coordinate falls under. A maximum of 25 Requests will be returned, sorted by recency of their creation. 

### HTTP Request

GET https://node.ucic.vc/api/v04/requests/nearest?lat=33.7490&lon=-84.3884

### Query Parameters

| Parameter | Type  | Description                 |
| --------- | ----- | --------------------------- |
| lat       | float | (Required) user's latitude  |
| lon       | float | (Required) user's longitude |

### Errors
| Error | Meaning                          |
| ----- | -------------------------------- |
| 400   | Missing required query parameter |

## Get Direct Requests

```shell
curl -X GET -H "Authorization: <AUTHORIZATION_TOKEN>" -H "Content-Type: application/json" "https://node.ucic.vc/api/v04/requests/direct"
```
```javascript

```

> The above command returns a 200 success code along with a json response like:

```json
[{ 
	"requestId": 51239,
	"message": "Can you show me what's happening there?",
	"start": "2017-03-28T18:45:33.286Z",
    "end": "2017-04-04T18:45:33.286Z",
	"requestType": 1,
    "responseCount": 2,
    "seen": true,
	"receiverUI": 39329,
    "discoverResponses": [{  // up to 3 entries in array
        "type": 0,
        "badge": "https://media.ucic.vc/assets/tags/CA.png",
      	"cardId": "F3A0F6F1-E61B-43E0-B78E-9309E0E60A55",
        "media": "https://media.ucic.vc/media/F3A0F6F1-E61B-43E0-B78E-9309E0E60A55/thumb.jpg"
    }],
	"creator": {
      "userId": 39266,
      "userName": "Billy Jean",
      "userAvatar": "http://staging-media.ucic.vc/media/B94667C1-19A6-4973-9003-9723A36BBF0F/thumb.jpg"
	}
}, ...]
```

Retrieve the direct requests for the authorized user.

### HTTP Request

GET https://node.ucic.vc/api/v04/requests/direct

## Get Specific Request By Id

```shell
curl -X GET -H "Authorization: <AUTHORIZATION_TOKEN>" -H "Content-Type: application/json" "https://node.ucic.vc/api/v04/requests/31832" 
```

```javascript

```
> The above command returns 200 success code along with a json response like:

```json
{ 
	"requestId": 51239,
	"message": "Can you show me what's happening there?",
	"start": "2017-03-28T18:45:33.286Z",
    "end": "2017-04-04T18:45:33.286Z",
	"requestType": 1,
    "responseCount": 3,
    "seen": false,
	"receiverUI": 39329,
    "discoverResponses": [{  // up to 3 entries in array
        "type": 0,
        "badge": "https://media.ucic.vc/assets/tags/CA.png",
      	"cardId": "F3A0F6F1-E61B-43E0-B78E-9309E0E60A55",
        "media": "https://media.ucic.vc/media/F3A0F6F1-E61B-43E0-B78E-9309E0E60A55/thumb.jpg"
    }],
	"creator": {
      "userId": 39266,
      "userName": "Billy Jean",
      "userAvatar": "http://staging-media.ucic.vc/media/B94667C1-19A6-4973-9003-9723A36BBF0F/thumb.jpg"
	}
}
```

> for a direct request and the following for a map request:

```json
{ 
	"requestId": 51239,
	"message": "Can you show me what's happening there?",
	"start": "2017-03-28T18:45:33.286Z",
    "end": "2017-04-04T18:45:33.286Z",
	"requestType": 0,
    "responseCount": 0,
    "seen": false,
    "discoverResponses": [{  // up to 3 entries in array
        "type": 0,
        "badge": "https://media.ucic.vc/assets/tags/CA.png",
      	"cardId": "F3A0F6F1-E61B-43E0-B78E-9309E0E60A55",
        "media": "https://media.ucic.vc/media/F3A0F6F1-E61B-43E0-B78E-9309E0E60A55/thumb.jpg"
    }],
	"location": {
      "lat": 33.7490,
      "lon": -84.3884,
      "radius": 525
	},
	"creator": {
      "userId": 39266,
      "userName": "Billy Jean",
      "userAvatar": "http://staging-media.ucic.vc/media/B94667C1-19A6-4973-9003-9723A36BBF0F/thumb.jpg"
	}
}
```
This endpoint retrieves a single Request by its id. 
**Note:** requestType specifies whether the Request is a Map Request (0), or Direct Request (1). The response type (image/video) is no longer decided in the Request, but by the responding client.

### HTTP Request

`GET https://node.ucic.vc/api/v04/requests/<ID>`


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

| Parameter | Type    | Description            |
| --------- | ------- | ---------------------- |
| seen      | Boolean | Seen status of request |


## Renew a Request

```shell
curl -X GET -H "Authorization: <AUTHORIZATION_TOKEN>" -H "Content-Type: application/json" "https://node.ucic.vc/api/v04/requests/renew/300106" 
```

```javascript
{
  
}
```

> The above command returns 200 on success along with a response structured as:

```json
{ 
	"newEnd": "2017-04-20T16:20:00.000Z"
}
```
> In the event of an error, the response will be structured as:

```json
{ 
	"error": "ERROR_CODE"
}
```

This endpoint allows the original creator of a request to extend the end date of the request to timeOfRequest + the default request lifespan (currently 7 days).

### HTTP Request

`GET https://node.ucic.vc/api/v04/requests/renew/<ID>`

### URL Parameters

| Parameter | Type    | Description                    |
| --------- | ------- | ------------------------------ |
| ID        | Integer | The id of the request to renew |

### Errors
| Error | Code              | Meaning                                  |
| ----- | ----------------- | ---------------------------------------- |
| 404   | REQUEST_NOT_FOUND | Specified request was not found          |
| 400   | NOT_REQUEST_OWNER | Specified request does not belong to the authorized user |

## Follow a Request

```shell
curl -X GET -H "Authorization: <AUTHORIZATION_TOKEN>" -H "Content-Type: application/json" "https://node.ucic.vc/api/v04/requests/follow/300106" 
```

```javascript

```

> The above command returns 204 on success


This endpoint allows a user to "follow" a request and receive alerts and push notifications when new responses are added to it.

### HTTP Request

`GET https://node.ucic.vc/api/v04/requests/follow/<ID>`

### URL Parameters

| Parameter | Type    | Description                    |
| --------- | ------- | ------------------------------ |
| ID        | Integer | The id of the request to renew |

## UnFollow a Request

```shell
curl -X GET -H "Authorization: <AUTHORIZATION_TOKEN>" -H "Content-Type: application/json" "https://node.ucic.vc/api/v04/requests/unfollow/300106" 
```

```javascript

```

> The above command returns 204 on success


This endpoint allows a user to stop "following" a request and no longer receive alerts and push notifications when new responses are added to it.

### HTTP Request

`GET https://node.ucic.vc/api/v04/requests/unfollow/<ID>`

### URL Parameters

| Parameter | Type    | Description                    |
| --------- | ------- | ------------------------------ |
| ID        | Integer | The id of the request to renew |
