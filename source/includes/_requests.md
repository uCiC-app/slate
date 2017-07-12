# Requests 

## Create and send a request 

```shell
curl -X POST -H "Authorization: <AUTHORIZATION_TOKEN>" -H "Content-Type: application/json" -d '{
    "location": {
        "lat": 33.7490,
        "lon": -84.3884,
        "radius": 750
    },
    "receiverUI": 197244,
    "questionId": "50b08a47-608f-41d6-a788-dcc9b34d3c9f",
    "message": "How are you doing today?",
    "override": false
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
| location\*   | { lat, lon, radius } | (Optional) location request lat lon coordinates and radius(m). |
| message      | String               | Request message content body (required)  |
| questionId   | String               | (Optional) The id of the question the user chose from the suggested questions list if they did not write their own. |
| override     | Boolean              | (Optional, default: false) Override time of day exception and send request anyway |
| receiverUI\* | Unsigned Integer     | (Optional) List of receiver user IDs     |

\* **Note:** The use of *location* or *receiverUI* or **neither** dictates what kind of request is created. If *receiverUI* is provided, it will become a direct request. If a *location* is provided, it'll become a map request (if both, a direct request). If neither is provided, it will become a global request.

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
    "questionId": "0d56a3c5-1c80-4de2-b151-d5d1f875ed6c",
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
    "discoverResponses": [{  // up to 10 entries in this array
        "type": 0,
        "badge": "https://media.ucic.vc/assets/tags/CA.png",
      	"cardId": "F3A0F6F1-E61B-43E0-B78E-9309E0E60A55",
        "media": "https://media.ucic.vc/media/F3A0F6F1-E61B-43E0-B78E-9309E0E60A55/thumb.jpg"
    }],
	"creator": {
      "userId": 39266,
      "userName": "Billy Jean",
      "badge": "https://media.ucic.vc/assets/tags/CA.png",
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
    "questionId": "0d56a3c5-1c80-4de2-b151-d5d1f875ed6c",
	"message": "Can you show me what's happening there?",
	"start": "2017-03-28T18:45:33.286Z",
    "end": "2017-04-04T18:45:33.286Z",
	"requestType": 1,
    "responseCount": 2,
    "seen": true,
	"receiverUI": 39329,
    "discoverResponses": [{  // up to 10 entries in array
        "type": 0,
        "badge": "https://media.ucic.vc/assets/tags/CA.png",
      	"cardId": "F3A0F6F1-E61B-43E0-B78E-9309E0E60A55",
        "media": "https://media.ucic.vc/media/F3A0F6F1-E61B-43E0-B78E-9309E0E60A55/thumb.jpg"
    }],
	"creator": {
      "userId": 39266,
      "userName": "Billy Jean",
      "badge": "https://media.ucic.vc/assets/tags/CA.png",
      "userAvatar": "http://staging-media.ucic.vc/media/B94667C1-19A6-4973-9003-9723A36BBF0F/thumb.jpg"
	}
}, ...]
```

Retrieve the direct requests for the authorized user.

### HTTP Request

GET https://node.ucic.vc/api/v04/requests/direct

## Get Global Requests

```shell
curl -X GET -H "Authorization: <AUTHORIZATION_TOKEN>" -H "Content-Type: application/json" "https://node.ucic.vc/api/v04/requests/global"
```
```javascript

```

> The above command returns a 200 success code along with a json response like:

```json
[{ 
	"requestId": 51239,
    "questionId": "0d56a3c5-1c80-4de2-b151-d5d1f875ed6c",
	"message": "Can you show me what's happening there?",
	"start": "2017-03-28T18:45:33.286Z",
    "end": "2017-04-04T18:45:33.286Z",
	"requestType": 2,
    "responseCount": 2,
    "seen": false,
    "discoverResponses": [{  // up to 10 entries in array
        "type": 0,
        "badge": "https://media.ucic.vc/assets/tags/CA.png",
      	"cardId": "F3A0F6F1-E61B-43E0-B78E-9309E0E60A55",
        "media": "https://media.ucic.vc/media/F3A0F6F1-E61B-43E0-B78E-9309E0E60A55/thumb.jpg"
    }],
	"creator": {
      "userId": 39266,
      "userName": "Billy Jean",
      "badge": "https://media.ucic.vc/assets/tags/CA.png",
      "userAvatar": "http://staging-media.ucic.vc/media/B94667C1-19A6-4973-9003-9723A36BBF0F/thumb.jpg"
	}
}, ...]
```

Retrieve global requests in order of most recent first. Route supports pagination.

### HTTP Request

GET https://node.ucic.vc/api/v04/requests/global

### Query Parameters

| Parameter | Type    | Description                              |
| --------- | ------- | ---------------------------------------- |
| limit     | Integer | Maximum number of requests to return     |
| offset    | Integer | Offset in list of requests to start return from |

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
    "questionId": "0d56a3c5-1c80-4de2-b151-d5d1f875ed6c",
	"message": "Can you show me what's happening there?",
	"start": "2017-03-28T18:45:33.286Z",
    "end": "2017-04-04T18:45:33.286Z",
	"requestType": 1,
    "responseCount": 3,
    "seen": false,
	"receiverUI": 39329,
    "discoverResponses": [{  // up to 10 entries in array
        "type": 0,
        "badge": "https://media.ucic.vc/assets/tags/CA.png",
      	"cardId": "F3A0F6F1-E61B-43E0-B78E-9309E0E60A55",
        "media": "https://media.ucic.vc/media/F3A0F6F1-E61B-43E0-B78E-9309E0E60A55/thumb.jpg"
    }],
	"creator": {
      "userId": 39266,
      "userName": "Billy Jean",
      "badge": "https://media.ucic.vc/assets/tags/CA.png",
      "userAvatar": "http://staging-media.ucic.vc/media/B94667C1-19A6-4973-9003-9723A36BBF0F/thumb.jpg"
	}
}
```

> for a direct request and the following for a map request:

```json
{ 
	"requestId": 51239,
    "questionId": "0d56a3c5-1c80-4de2-b151-d5d1f875ed6c",
	"message": "Can you show me what's happening there?",
	"start": "2017-03-28T18:45:33.286Z",
    "end": "2017-04-04T18:45:33.286Z",
	"requestType": 0,
    "responseCount": 0,
    "seen": false,
    "discoverResponses": [{  // up to 10 entries in array
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
      "badge": "https://media.ucic.vc/assets/tags/CA.png",
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

> The above command returns 204 on success

This endpoint updates the current user's request's status.

### HTTP Request

`PUT https://node.ucic.vc/api/v04/requests/<ID>`

### Body Parameters

| Parameter | Type    | Description            |
| --------- | ------- | ---------------------- |
| seen      | Boolean | Seen status of request |

##Update multiple request's seen status
```shell
curl -X PUT -H "Authorization: <AUTHORIZATION_TOKEN>" -H "Content-Type: application/json" -d '{ "requestIds": ['300102', '300120'] }' "https://node.ucic.vc/api/v04/requests/bulkSeen" 
```
```javascript

```
> The above command returns 204 on success

This endpoint updates the current user's request's status to seen for all provided request identifiers.

### HTTP Request

`PUT https://node.ucic.vc/api/v04/requests/bulkSeen`

### Body Parameters

| Parameter  | Type         | Description                              |
| ---------- | ------------ | ---------------------------------------- |
| requestIds | String Array | Array of request identifiers which will be marked as seen |

### Errors
| Error | Meaning                                  |
| ----- | ---------------------------------------- |
| 400   | Missing required field. Sent if requestIds is not present, or is not an array |

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

| Parameter | Type    | Description                     |
| --------- | ------- | ------------------------------- |
| ID        | Integer | The id of the request to follow |

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

| Parameter | Type    | Description                       |
| --------- | ------- | --------------------------------- |
| ID        | Integer | The id of the request to unfollow |

## Skip a Request

```shell
curl -X PUT -H "Authorization: <AUTHORIZATION_TOKEN>" -H "Content-Type: application/json" "https://node.ucic.vc/api/v04/requests/skip/300106" 
```

```javascript

```

> The above command returns 204 on success


This endpoint allows a user to "skip" a request and have it permanently removed from the results of the various GET request endpoints for this user.

### HTTP Request

`PUT https://node.ucic.vc/api/v04/requests/skip/<ID>`

### URL Parameters

| Parameter | Type    | Description                   |
| --------- | ------- | ----------------------------- |
| ID        | Integer | The id of the request to skip |