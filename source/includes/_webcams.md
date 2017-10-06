# Webcams

## Get single webcam info

```shell
curl -H "Authorization: <AUTHORIZATION_TOKEN>" "https://node.ucic.vc/api/v04/webcam/1183551354"
```
```javascript

```

> The above command returns a 204 status code upon success

```json
{
  "views": 243,
  "posts": 1,
  "id": "1183551354",
  "title": "San Francisco: Golden Gate Bridge − San Francisco Bay",
  "lat": 37.805122,
  "lon": -122.450695,
  "countryCode": "US",
  "region": "California",
  "city": "San Francisco",
  "timezone": "America/Los_Angeles"
}
```

Fetches the info for a single webcam room by id.

### HTTP Request

`GET https://node.ucic.vc/api/v04/webcam/:webcamId`

### URL Parameters

| Parameter | Type   | Description                           |
| --------- | ------ | ------------------------------------- |
| webcamId  | String | The identifier of the webcam to fetch |

### Errors

| Code | Error                        | Description                              |
| ---- | ---------------------------- | ---------------------------------------- |
| 404  | webcam not found with id :id | Could not match the id the client sent to a webcam |

## Get Webcam Room media items

```shell
curl -H "Authorization: <AUTHORIZATION_TOKEN>" "https://node.ucic.vc/api/v04/webcam/1183551354/media"
```
```javascript

```

> The above command returns a 204 status code upon success

```json
{
  "id": "9741cb8d-de9e-4613-9259-1ca8e27949d5",
  "webcamId": "1183551354",
  "timestamp": "2017-10-05T18:52:36.000Z",
  "imageUrl": "https://media.ucic.vc/webcamMedia/1183551354/1507229556.jpg",
  "likeCount": 1,
  "liked": true,
  "commentCount": 0
}
```

Fetches the media objects for a single webcam room by id.  
**Note:** There should always be at least one WebcamMedia item.  
When liking/commenting on the item, use the `.id` parameter as the `itemId` with an `itemType` of `webcamMedia`  
**Note2:** In order to guarantee that at least one item exists and that it's (reasonably) up to date, the call to fetch the first page of webcam media for a given room may be a bit slow as it is checking the first item in the room against the webcam api to see if it need to create a new one (and optionally delete the old one). 

### HTTP Request

`GET https://node.ucic.vc/api/v04/webcam/:webcamId/media`

### URL Parameters

| Parameter | Type   | Description                              |
| --------- | ------ | ---------------------------------------- |
| webcamId  | String | The identifier of the webcam to fetch media for |

### Query Parameters

| Parameter | Type    | Description                              |
| --------- | ------- | ---------------------------------------- |
| limit     | Integer | Maximum number of media items to return at once |
| offset    | Integer | How many items to skip in the return     |

