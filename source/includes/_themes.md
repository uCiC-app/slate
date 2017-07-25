#Themes 

## Get Themes by Country

```shell
curl "https://node.ucic.vc/api/v05/themes/get" -H "Authorization: <AUTHORIZATION_TOKEN>"
```

```javascript

```

> The above command returns JSON structured like this:

```json
[
  {
    "id": "E73CD7C4-35E7-4A37-9850-950E22B2BCCF",
    "name": "United States of America",
    "maxLikes": "78",
    "logo": "http://staging-media.ucic.vc/assets/tags/US.png"
  }
]
```

This endpoint retrieves all themes.

### HTTP Request

`GET https://node.ucic.vc/api/v05/themes`

### Query Parameters

| Parameter | Default          | Description                              |
| --------- | ---------------- | ---------------------------------------- |
| limit     | Unsigned Integer | Maximum number of themes to return       |
| offset    | Unsigned Integer | Offset in list of themes to start return from |
| page      | Unsigned Integer | Page of themes to return                 |
| sort      | String           | Sort of results.  'random' sorts randomly and returns a Sort-Seed header with the random sort seed.  'likes' sorts by likes descending.  Default is sort by likes descending. |
| seed      | UUID             | Sorting seed for random sorting.  Returned as header when a random sort is requested |

<aside class="success">
Remember — a happy uCiC client is an authenticated uCiC client!
</aside>

## Get Themes by Request

```shell
curl "https://node.ucic.vc/api/v05/themes/requests" -H "Authorization: <AUTHORIZATION_TOKEN>"
```

```javascript

```

> The above command returns JSON structured like this:

```json
[
  {
    "requestId": "300123",
    "questionId": "a29c2a61-7fee-492e-80e6-907c859b4419",
    "message": "What's going on over there?",
    "start": "2017-04-24T13:42:39.000Z",
    "end": "2017-05-01T13:42:39.000Z",
    "requestType": 0,
    "responseCount": 5,
    "followers": [
      {
        "userId": 414383,
        "userName": "Safe 2",
        "userAvatar": "https://media.ucic.vc/media/F77318CA-AD36-4BC2-9EF1-607A76051E3F/thumb.jpg"
      }
    ],
    "discoverResponses": [  // up to 10 entries in this array
      {
        "type": 0,
        "badge": "https://media.ucic.vc/assets/tags/CA.png",
        "caption": "some text that's part of the response",
        "cardId": "87F5E446-4395-4034-99F0-EF14A3E8FD39",
        "media": "https://media.ucic.vc/media/87F5E446-4395-4034-99F0-EF14A3E8FD39/thumb.jpg",
        "displayMedia": "https://media.ucic.vc/media/87F5E446-4395-4034-99F0-EF14A3E8FD39/display.jpg"
      },
      {
        "type": 0,
        "badge": "https://media.ucic.vc/assets/tags/CA.png",
        "caption": "some text that's part of the response",
        "cardId": "992D8E8E-EDE0-42BF-97B0-2940D91E7CA0",
        "media": "https://media.ucic.vc/media/992D8E8E-EDE0-42BF-97B0-2940D91E7CA0/thumb.jpg",
        "displayMedia": "https://media.ucic.vc/media/992D8E8E-EDE0-42BF-97B0-2940D91E7CA0/display.jpg"
      },
      {
        "type": 0,
        "badge": "https://media.ucic.vc/assets/tags/CA.png",
        "caption": "some text that's part of the response",
        "cardId": "033FE824-97E1-4458-80D6-B1ED62902380",
        "media": "https://media.ucic.vc/media/033FE824-97E1-4458-80D6-B1ED62902380/thumb.jpg",
        "displayMedia": "https://media.ucic.vc/media/033FE824-97E1-4458-80D6-B1ED62902380/display.jpg"
      }
    ],
    "creator": {
      "userId": 414383,
      "userName": "Safe 2",
      "badge": "https://media.ucic.vc/assets/tags/CA.png",
      "userAvatar": "https://media.ucic.vc/media/F77318CA-AD36-4BC2-9EF1-607A76051E3F/thumb.jpg"
    },
    "location": {         // only present when requestType = 0
      "lat": 43.4555,
      "lon": -80.3977,
      "radius": 10000
    },
    "receiverUI": 414380  // only present when requestType = 1
  }
]
```

This endpoint retrieves all themes based on Requests. The most recently responded-to requests are shown first. The field _discoverResponses_ contains data for up to 10 responses to the request, sorted by most recent first.

### HTTP Request

`GET https://node.ucic.vc/api/v05/themes/requests`

### Query Parameters

| Parameter | Type             | Description                              |
| --------- | ---------------- | ---------------------------------------- |
| limit     | Unsigned Integer | Maximum number of themes to return       |
| offset    | Unsigned Integer | Offset in list of themes to start return from |
| sort      | String<'latestResponse:desc','totalLikes:desc','latestLike:desc' | Sort order, default is 'latestResponse:desc'

## Get Themes by Question

```shell
curl "https://node.ucic.vc/api/v05/themes/questions" -H "Authorization: <AUTHORIZATION_TOKEN>"
```

```javascript

```

> The above command returns JSON structured like this:

```json
[
  {
    "requestId": "300123",
    "questionId": "a29c2a61-7fee-492e-80e6-907c859b4419",
    "message": "What's going on over there?",
    "start": "2017-04-24T13:42:39.000Z",
    "end": "2017-05-01T13:42:39.000Z",
    "requestType": 0,
    "responseCount": 5,
    "followers": [
      {
        "userId": 414383,
        "userName": "Safe 2",
        "userAvatar": "https://media.ucic.vc/media/F77318CA-AD36-4BC2-9EF1-607A76051E3F/thumb.jpg"
      }
    ],
    "discoverResponses": [  // up to 10 entries in this array
      {
        "type": 0,
        "badge": "https://media.ucic.vc/assets/tags/CA.png",
        "cardId": "87F5E446-4395-4034-99F0-EF14A3E8FD39",
        "caption": "some text that's part of the response",
        "media": "https://media.ucic.vc/media/87F5E446-4395-4034-99F0-EF14A3E8FD39/thumb.jpg",
        "displayMedia": "https://media.ucic.vc/media/87F5E446-4395-4034-99F0-EF14A3E8FD39/display.jpg"
      },
      {
        "type": 0,
        "badge": "https://media.ucic.vc/assets/tags/CA.png",
        "cardId": "992D8E8E-EDE0-42BF-97B0-2940D91E7CA0",
        "caption": "some text that's part of the response",
        "media": "https://media.ucic.vc/media/992D8E8E-EDE0-42BF-97B0-2940D91E7CA0/thumb.jpg",
        "displayMedia": "https://media.ucic.vc/media/992D8E8E-EDE0-42BF-97B0-2940D91E7CA0/display.jpg"
      },
      {
        "type": 0,
        "badge": "https://media.ucic.vc/assets/tags/CA.png",
        "cardId": "033FE824-97E1-4458-80D6-B1ED62902380",
        "caption": "some text that's part of the response",
        "media": "https://media.ucic.vc/media/033FE824-97E1-4458-80D6-B1ED62902380/thumb.jpg",
        "displayMedia": "https://media.ucic.vc/media/033FE824-97E1-4458-80D6-B1ED62902380/display.jpg"
      }
    ],
    "creator": {
      "userId": 414383,
      "userName": "Safe 2",
      "badge": "https://media.ucic.vc/assets/tags/CA.png",
      "userAvatar": "https://media.ucic.vc/media/F77318CA-AD36-4BC2-9EF1-607A76051E3F/thumb.jpg"
    },
    "location": {         // only present when requestType = 0
      "lat": 43.4555,
      "lon": -80.3977,
      "radius": 10000
    },
    "receiverUI": 414380  // only present when requestType = 1
  }
]
```

This endpoint retrieves all themes based on Question ID. The most recently responded-to questions are shown first. The field _discoverResponses_ contains data for up to 10 responses to the request, sorted by most recent first.

### HTTP Request

`GET https://node.ucic.vc/api/v05/themes/questions`

### Query Parameters

| Parameter | Type                                     | Description                              |
| --------- | ---------------------------------------- | ---------------------------------------- |
| limit     | Unsigned Integer                         | Maximum number of themes to return       |
| offset    | Unsigned Integer                         | Offset in list of themes to start return from |
| sort      | String<'latestResponse:desc','latestLike:desc'> | Sort order, default is 'latestResponse:desc' |

## Get a Specific Theme 

```shell
curl "https://node.ucic.vc/api/v05/themes/928CF4AC-A5BF-4A8B-8C47-62E58AE1F655" -H "Authorization: <AUTHORIZATION_TOKEN>"
```

```javascript

```

> The above command returns JSON structured like this:

```json
{
  "id": "928CF4AC-A5BF-4A8B-8C47-62E58AE1F655",
  "name": "Canada",
  "maxLikes": "28",
  "logo": "http://staging-media.ucic.vc/assets/tags/CA.png"
}
```

This endpoint retrieves a specific theme.

### HTTP Request

`GET https://node.ucic.vc/api/v05/themes/<ID>`

### URL Parameters

| Parameter | Type | Description                     |
| --------- | ---- | ------------------------------- |
| ID        | UUID | The ID of the theme to retrieve |


## Get Themes for Followed Items

```shell
curl "https://node.ucic.vc/api/v05/themes/following" -H "Authorization: <AUTHORIZATION_TOKEN>"
```

```javascript

```

> The above command returns JSON structured like this:

```json

[{
  "type": "q",  // or 'user'
  "refId": "2793219a-9cf7-451f-92a3-04a12fe3d270",
  "message": "What you are looking at?",
  "responseCount": 24,
  "followers": [{
    "userId": 414375,
    "userName": "The North",
    "avatar": "https://media.ucic.vc/media/F77318CA-AD36-4BC2-9EF1-607A76051E3F/thumb.jpg"
  }],
  "discoverResponses": [{
    "type": 0,
    "badge": "https://media.ucic.vc/assets/tags/CA.png",
    "caption": "",
    "cardId": "CEC62D28-950D-4AE3-830D-21E05C48AD3A",
    "media": "https://media.ucic.vc/media/CEC62D28-950D-4AE3-830D-21E05C48AD3A/thumb.jpg",
    "displayMedia": "https://media.ucic.vc/media/CEC62D28-950D-4AE3-830D-21E05C48AD3A/display.jpg"
  }],
  "creator": {
    "userId": 414739,
    "userName": "Jan Snow",
    "userAvatar": "https://media.ucic.vc/media/default/thumb.jpg",
    "badge": "https://media.ucic.vc/assets/tags/CA.png"
  }
}]
```

This endpoint retrieves themes based on the various entities that the authorized user follows, sorted by most recent response first. In addition to the data returned by other theme GET routes, two additional fields are provided to distinguish *what* the theme is for. These fields are `type` and `refId`. The `type` field currently has 2 possible values: 'q' and 'user' to indicate a theme for a followed question or user, respectively. The `refId` field in turn, specifies the unique identifier of the question or user that the theme refers to, so that the client can then open the full card set for that theme with either a call to GET /questions/:refId/cards, or GET users/:refId/responses. 

**Special considerations:** generating the following theme is very computationally expensive per page, and involves throwing away a bit of work during each call. Further, due to the limitations of Elasticsearch's Aggregation implementation, there is a slightly increased chance of repeated or missed rows at the borders of "pages". As such, it is recommended that the clients use a slightly larger page size (say, 15 instead of 10 rows per call) for this theme to lower the overall load on the server and decrease the chances that they encounter pagination related row discrepencies.

### HTTP Request

`GET https://node.ucic.vc/api/v05/themes/following`

### Query Parameters

| Parameter | Type             | Description                              |
| --------- | ---------------- | ---------------------------------------- |
| limit     | Unsigned Integer | Maximum number of themes to return       |
| offset    | Unsigned Integer | Offset in list of themes to start return from |

## Search for a Theme 

```shell
curl "https://node.ucic.vc/api/v05/themes/search?query=Boliv" -H "Authorization: <AUTHORIZATION_TOKEN>"
```

```javascript

```

> The above command returns JSON structured like this:

```json
[
  {
    "name": "Bolivia",
    "id": "EF60D822-67DB-4E2D-8F01-4B31F54AF21E"
  }
]
```

This endpoint searches for themes matching their title against the provided query.

### HTTP Request

`GET https://node.ucic.vc/api/v05/themes/search?query=<SEARCH_QUERY>`

### Query Parameters

| Parameter | Type   | Description                              |
| --------- | ------ | ---------------------------------------- |
| query     | String | The search substring to find matching themes for |


