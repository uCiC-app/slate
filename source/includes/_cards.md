#Cards 

## Get the Cards for a Theme 

```shell
curl "https://node.ucic.vc/api/v05/themes/928CF4AC-A5BF-4A8B-8C47-62E58AE1F655/cards" -H "Authorization: <AUTHORIZATION_TOKEN>"
```

```javascript

```

> The above command returns JSON structured like this:

```json
[
  {
    "id": "4F211D7B-5DA4-42FA-9C44-E8CEAB4C05EC",
    "tagId": "928CF4AC-A5BF-4A8B-8C47-62E58AE1F655",
    "comments": [{
      "id": "a8c1236a-5ab1-4874-b25e-3aeebdc15909",
        "text": "This is a comment ",
        "itemId": "4F211D7B-5DA4-42FA-9C44-E8CEAB4C05EC",
        "itemType": "card",
        "createdAt": "2017-06-09 19:47:43",
        "likeCount": 7,
        "liked": true,
        "creator": {
          "UI": "195502",
          "avatar": "https://media.ucic.vc/media/7C21E547-277A-4A23-934A-E7986B82E5EB/micro.jpg",
          "Username": "Jay Jay",
          "badge": "https://media.ucic.vc/assets/tags/CA.png"
         }
    }],
    "request": {
      "id": "40839",
      "body": "Anything interesting to see around you?",
      "createdAt": "2016-04-22T01:02:37.000Z",
      "likeCount": 3,
      "liked": false,
      "requestType": 0,   // 0 = map, 1 = direct, 2 = global
      "sender": {
        "id": "36001",
        "fullname": "Jack Liu",
        "badge": "https://media.ucic.vc/assets/tags/CA.png",
        "avatar": "http://staging-media.ucic.vc/media/default/thumb.png"
      }
    },
    "response": {
      "id": "14062",
      "body": "Mural",
      "createdAt": "2016-04-22T01:29:23.530Z",
      "sender": {
        "id": "71",
        "fullname": "Ashley",
        "badge": "https://media.ucic.vc/assets/tags/CA.png",
        "avatar": "http://staging-media.ucic.vc/media/default/thumb.png"
      },
      "media": {
        "id": "4F211D7B-5DA4-42FA-9C44-E8CEAB4C05EC",
        "mi": "11831",
        "url": "http://staging-media.ucic.vc/media/4F211D7B-5DA4-42FA-9C44-E8CEAB4C05EC/original.jpg",
        "display": "http://staging-media.ucic.vc/media/4F211D7B-5DA4-42FA-9C44-E8CEAB4C05EC/display.jpg",
        "thumb": "http://staging-media.ucic.vc/media/4F211D7B-5DA4-42FA-9C44-E8CEAB4C05EC/thumb.jpg",
        "lat": 43.4513854980469,
        "lon": -80.498664855957,
        "mimeType": "image/jpeg",
        "likes": 28,
        "badge": "https://media.ucic.vc/assets/tags/RU.png",
        "liked": false,
        "createdAt": "2016-04-22T01:29:37.000Z",
        "metaData": {
          "city": "Mozhaysk",
          "region": "Moskovskaya oblast'",
          "country": "Russia",
          "uploaded": 1,  // 0 = captured in-app, 1 = attached
          "createdAt": "2017-01-25T12:00:00.000Z",
          "location": {
            "lat": 47.45,
            "lon": 6.93546
          }
        },
        "tags": [
          {
            "id": "E73CD7C4-35E7-4A37-9850-950E22B2BCCF",
            "category": "country",
            "name": "United States of America"
          },
          {
            "id": "F8E5FF35-3CAD-462C-B115-3E0D0B0DF4D7",
            "category": "vision",
            "name": "spaniel"
          }
        ]
      }
    }
  }
]
```

This endpoint retrieves the cards for a theme.

### HTTP Request

`GET https://node.ucic.vc/api/v05/themes/<ID>/cards`

### URL Parameters

| Parameter | Type | Description                              |
| --------- | ---- | ---------------------------------------- |
| ID        | UUID | The ID of the theme to retrieve cards for |

### Query Parameters

| Parameter | Type             | Description                              |
| --------- | ---------------- | ---------------------------------------- |
| limit     | Unsigned Integer | Maximum number of cards to return        |
| offset    | Unsigned Integer | Offset in list of cards to start return from |
| page      | Unsigned Integer | Page of cards to return                  |
| sort      | String           | Sort by 'createdAt' or likes'.  Default is 'likes' |
| order     | String           | Direction of sort, either 'ASC' for ascending or 'DESC' for descending, default is DESC |
| cutoff    | unsigned Integer | Restrict the scope of the query to the cutoff number of cards |
| cutoffBy  | String           | Scopes the query to the largest likes or the most recent cutoff documents.  'likes' or 'createdAt' are supported.  Default is 'createdAt'. |

## Get a Specific Card 

```shell
curl "https://node.ucic.vc/api/v05/cards/DEC604AC-C29F-4764-B9C6-2CEC7351ABB6" -H "Authorization: <AUTHORIZATION_TOKEN>"
```

```javascript

```

> The above command returns JSON structured like this:

```json
{
  "id": "F48F16C0-81BE-418D-B44B-9F97DD2D3A70",
  "tagId": "928CF4AC-A5BF-4A8B-8C47-62E58AE1F655",
  "comments": [{
    "id": "a8c1236a-5ab1-4874-b25e-3aeebdc15909",
    "text": "This is a comment ",
    "itemId": "F48F16C0-81BE-418D-B44B-9F97DD2D3A70",
    "itemType": "card",
    "likeCount": 7,
    "liked": true,
    "createdAt": "2017-06-09 19:47:43",
    "creator": {
      "UI": "195502",
      "avatar": "https://media.ucic.vc/media/7C21E547-277A-4A23-934A-E7986B82E5EB/micro.jpg",
      "Username": "Jay Jay",
      "badge": "https://media.ucic.vc/assets/tags/CA.png"
    }
  }],
  "request": {
    "id": "46154",
    "body": "How's the sunset there?",
    "createdAt": "2016-12-09T22:40:22.100Z",
    "likeCount": 7,
    "liked": true,
    "requestType": 0,   // 0 = map, 1 = direct, 2 = global, 3 = event
    "sender": {
      "id": "38988",
      "fullname": "Falak",
      "badge": "https://media.ucic.vc/assets/tags/CA.png",
      "avatar": "http://staging-media.ucic.vc/media/default/thumb.png"
    }
  },
  "response": {
    "id": "15958",
    "body": "Very Pretty!",
    "createdAt": "2016-12-09T22:40:22.100Z",
    "sender": {
      "id": "39124",
      "fullname": "Gbs",
      "badge": "https://media.ucic.vc/assets/tags/CA.png",
      "avatar": "http://staging-media.ucic.vc/media/default/thumb.png"
    },
    "media": {
      "id": "F48F16C0-81BE-418D-B44B-9F97DD2D3A70",
      "mi": "13370",
      "url": "http://staging-media.ucic.vc/media/F48F16C0-81BE-418D-B44B-9F97DD2D3A70/original.png",
      "display": "http://staging-media.ucic.vc/media/F48F16C0-81BE-418D-B44B-9F97DD2D3A70/display.jpg",
      "thumb": "http://staging-media.ucic.vc/media/F48F16C0-81BE-418D-B44B-9F97DD2D3A70/thumb.png",
      "lat": 43.4531783,
      "lon": -80.495723,
      "mimeType": "image/png",
      "likes": 10,
      "badge": "https://media.ucic.vc/assets/tags/RU.png",
      "liked": false,
      "createdAt": "2016-12-10T01:58:01.653Z",
      "metaData": {
        "city": "Mozhaysk",
        "region": "Moskovskaya oblast'",
        "country": "Russia",
        "uploaded": 1,
        "createdAt": "2016-01-25T12:00:00.000Z",
        "location": {
          "lat": 47.45,
          "lon": 6.93546
        }
      },
      "tags": [
        {
          "id": "E73CD7C4-35E7-4A37-9850-950E22B2BCCF",
          "category": "country",
          "name": "United States of America"
        },
        {
          "id": "F8E5FF35-3CAD-462C-B115-3E0D0B0DF4D7",
          "category": "vision",
          "name": "spaniel"
        }
      ]
    }
  }
}
```

This endpoint retrieves a specific card.

### HTTP Request

`GET https://node.ucic.vc/api/v05/cards/<ID>`

### URL Parameters

| Parameter | Type | Description                    |
| --------- | ---- | ------------------------------ |
| ID        | UUID | The ID of the card to retrieve |


## Get User's Requested Cards

```shell
curl "https://node.ucic.vc/api/v04/users/requests" -H "Authorization: <AUTHORIZATION_TOKEN>"

curl "https://node.ucic.vc/api/v04/users/<ID>/requests" -H "Authorization: <AUTHORIZATION_TOKEN>"
```

```javascript

```

> The above command returns JSON structured like this:

```json
[
  {
    "id": "88F95DFB-0080-40F1-9529-55FBB74FC55D",
    "tagId": "928CF4AC-A5BF-4A8B-8C47-62E58AE1F655",
    "comments": [{
      "id": "a8c1236a-5ab1-4874-b25e-3aeebdc15909",
      "text": "This is a comment ",
      "itemId": "88F95DFB-0080-40F1-9529-55FBB74FC55D",
      "itemType": "card",
      "likeCount": 7,
      "liked": true,
      "createdAt": "2017-06-09 19:47:43",
      "creator": {
        "UI": "195502",
        "avatar": "https://media.ucic.vc/media/7C21E547-277A-4A23-934A-E7986B82E5EB/micro.jpg",
        "Username": "Jay Jay",
        "badge": "https://media.ucic.vc/assets/tags/CA.png"
      }
    }],
    "request": {
      "id": "45691",
      "body": "How is the beach there?",
      "createdAt": "2016-11-28T18:15:15.166Z",
      "likeCount": 3,
      "liked": false,
      "requestType": 2,   // 0 = map, 1 = direct, 2 = global, 3 = event
      "sender": {
        "id": "611",
        "fullname": "John Doe",
        "badge": "https://media.ucic.vc/assets/tags/CA.png",
        "avatar": "http://staging-media.ucic.vc/media/default/thumb.png"
      }
    },
    "response": {
      "id": "15790",
      "body": "Ain't no beaches round here",
      "createdAt": "2016-11-28T18:15:15.166Z",
      "sender": {
        "id": "39086",
        "fullname": "yhhji",
        "badge": "https://media.ucic.vc/assets/tags/CA.png",
        "avatar": "http://staging-media.ucic.vc/media/default/thumb.png"
      },
      "media": {
        "id": "88F95DFB-0080-40F1-9529-55FBB74FC55D",
        "mi": "13254",
        "url": "http://staging-media.ucic.vc/media/88F95DFB-0080-40F1-9529-55FBB74FC55D/original.jpg",
        "display": "http://staging-media.ucic.vc/media/88F95DFB-0080-40F1-9529-55FBB74FC55D/display.jpg",
        "thumb": "http://staging-media.ucic.vc/media/88F95DFB-0080-40F1-9529-55FBB74FC55D/thumb.jpg",
        "lat": 43.45162600766234,
        "lon": -80.4984725455851,
        "mimeType": "image/jpeg",
        "likes": 10,
        "badge": "https://media.ucic.vc/assets/tags/RU.png",
        "liked": false,
        "createdAt": "2016-11-30T00:57:14.213Z",
        "metaData": {
          "city": "Mozhaysk",
          "region": "Moskovskaya oblast'",
          "country": "Russia",
          "uploaded": 1,
          "createdAt": "2016-01-25T12:00:00.000Z",
          "location": {
            "lat": 47.45,
            "lon": 6.93546
          }
        },
        "tags": [
          {
            "id": "E73CD7C4-35E7-4A37-9850-950E22B2BCCF",
            "category": "country",
            "name": "United States of America"
          },
          {
            "id": "F8E5FF35-3CAD-462C-B115-3E0D0B0DF4D7",
            "category": "vision",
            "name": "spaniel"
          }
        ]
      }
    }
  }
]
```

This endpoint retrieves the cards that a user has requested.

### HTTP Request

`GET https://node.ucic.vc/api/v04/users/requests`

`GET https://node.ucic.vc/api/v04/users/611/requests`

### Route parameters
| Parameter | Type             | Description                          |
| --------- | ---------------- | ------------------------------------ |
| ID        | Unsigned Integer | Optional. User's id to get cards for |

### Query Parameters

| Parameter | Type             | Description                              |
| --------- | ---------------- | ---------------------------------------- |
| limit     | Unsigned Integer | Maximum number of comments to return     |
| offset    | Unsigned Integer | Offset in list of commentss to start return from |
| page      | Unsigned Integer | Page of comments to return               |
| sort      | String           | Sort by 'createdAt' or likes'.  Default is 'likes' |
| order     | String           | Direction of sort, either 'ASC' for ascending or 'DESC' for descending, default is DESC |


## Get User's Responded Cards

```shell
curl "https://node.ucic.vc/api/v04/users/responses" -H "Authorization: <AUTHORIZATION_TOKEN>"

curl "https://node.ucic.vc/api/v04/users/<ID>/responses" -H "Authorization: <AUTHORIZATION_TOKEN>"
```

```javascript

```

> The above command returns JSON structured like this:

```json
[
  {
    "id": "08241390-F145-4245-A68A-5D7852488673",
    "tagId": "4F45AA05-0522-4674-8178-FE9983DE4BC4",
    "comments": [{
      "id": "a8c1236a-5ab1-4874-b25e-3aeebdc15909",
      "text": "This is a comment ",
      "itemId": "08241390-F145-4245-A68A-5D7852488673",
      "itemType": "card",
      "likeCount": 7,
      "liked": true,
      "createdAt": "2017-06-09 19:47:43",
      "creator": {
        "UI": "195502",
        "avatar": "https://media.ucic.vc/media/7C21E547-277A-4A23-934A-E7986B82E5EB/micro.jpg",
        "Username": "Jay Jay",
        "badge": "https://media.ucic.vc/assets/tags/CA.png"
      }
    }],
    "request": {
      "id": "45220",
      "body": "What's something you show your out of twon guests?",
      "createdAt": "2016-11-08T23:01:13.260Z",
      "requestType": 0,   // 0 = map, 1 = direct, 2 = global, 3 = event
      "likeCount": 1,
      "liked": false,
      "sender": {
        "id": "38992",
        "fullname": "duty3test",
        "badge": "https://media.ucic.vc/assets/tags/CA.png",
        "avatar": "http://staging-media.ucic.vc/media/default/thumb.png"
      }
    },
    "response": {
      "id": "15957",
      "body": "Hi There!",
      "createdAt": "2016-11-08T23:01:13.260Z",
      "sender": {
        "id": "611",
        "fullname": "John Doe",
        "badge": "https://media.ucic.vc/assets/tags/CA.png",
        "avatar": "http://staging-media.ucic.vc/media/default/thumb.png"
      },
      "media": {
        "id": "08241390-F145-4245-A68A-5D7852488673",
        "mi": "13369",
        "url": "http://staging-media.ucic.vc/media/08241390-F145-4245-A68A-5D7852488673/original.mp4",
        "display": "http://staging-media.ucic.vc/media/08241390-F145-4245-A68A-5D7852488673/display.jpg",
        "thumb": "http://staging-media.ucic.vc/media/2A6F06F8-6CCE-45AE-9920-D7F7D515E31B/thumb.png",
        "lat": -22.9035393,
        "lon": -43.2095869,
        "mimeType": "video/mp4",
        "likes": 10,
        "badge": "https://media.ucic.vc/assets/tags/RU.png",
        "liked": true,
        "createdAt": "2016-12-09T19:50:12.830Z",
        "metaData": {
          "city": "Mozhaysk",
          "region": "Moskovskaya oblast'",
          "country": "Russia",
          "uploaded": 0,
          "createdAt": "2016-01-25T12:00:00.000Z",
          "location": {
            "lat": 47.45,
            "lon": 6.93546
          }
        },
        "tags": [
          {
            "id": "E73CD7C4-35E7-4A37-9850-950E22B2BCCF",
            "category": "country",
            "name": "United States of America"
          },
          {
            "id": "F8E5FF35-3CAD-462C-B115-3E0D0B0DF4D7",
            "category": "vision",
            "name": "spaniel"
          }
        ]
      }
    }
  }
]
```

This endpoint retrieves the cards that the current user has responded to requests with.

### HTTP Request

`GET https://node.ucic.vc/api/v04/users/responses`

`GET https://node.ucic.vc/api/v04/users/611/responses`


### Route parameters
| Parameter | Type             | Description                          |
| --------- | ---------------- | ------------------------------------ |
| ID        | Unsigned Integer | Optional. User's id to get cards for |

### Query Parameters

| Parameter | Type             | Description                              |
| --------- | ---------------- | ---------------------------------------- |
| limit     | Unsigned Integer | Maximum number of comments to return     |
| offset    | Unsigned Integer | Offset in list of commentss to start return from |
| page      | Unsigned Integer | Page of comments to return               |
| sort      | String           | Sort by 'createdAt' or likes'.  Default is 'likes' |
| order     | String           | Direction of sort, either 'ASC' for ascending or 'DESC' for descending, default is DESC |

## Get the Cards for a Request 

```shell
curl "https://node.ucic.vc/api/v04/requests/300106/cards" -H "Authorization: <AUTHORIZATION_TOKEN>"
```

```javascript

```

> The above command returns JSON structured like this:

```json
[
  {
    "id": "4F211D7B-5DA4-42FA-9C44-E8CEAB4C05EC",
    "tagId": "928CF4AC-A5BF-4A8B-8C47-62E58AE1F655",
    "comments": [{
      "id": "a8c1236a-5ab1-4874-b25e-3aeebdc15909",
      "text": "This is a comment ",
      "itemId": "4F211D7B-5DA4-42FA-9C44-E8CEAB4C05EC",
      "itemType": "card",
      "likeCount": 7,
      "liked": true,
      "createdAt": "2017-06-09 19:47:43",
      "creator": {
        "UI": "195502",
        "avatar": "https://media.ucic.vc/media/7C21E547-277A-4A23-934A-E7986B82E5EB/micro.jpg",
        "Username": "Jay Jay",
        "badge": "https://media.ucic.vc/assets/tags/CA.png"
      }
    }],
    "request": {
      "id": "40839",
      "body": "Anything interesting to see around you?",
      "createdAt": "2016-04-22T01:02:37.000Z",
      "requestType": 0,   // 0 = map, 1 = direct, 2 = global, 3 = event
      "following": true,
      "likeCount": 2,
      "liked": false,
      "sender": {
        "id": "36001",
        "fullname": "Jack Liu",
        "badge": "https://media.ucic.vc/assets/tags/CA.png",
        "avatar": "http://staging-media.ucic.vc/media/default/thumb.png"
      }
    },
    "response": {
      "id": "14062",
      "body": "Mural",
      "createdAt": "2016-04-22T01:29:23.530Z",
      "sender": {
        "id": "71",
        "fullname": "Ashley",
        "badge": "https://media.ucic.vc/assets/tags/CA.png",
        "avatar": "http://staging-media.ucic.vc/media/default/thumb.png"
      },
      "media": {
        "id": "4F211D7B-5DA4-42FA-9C44-E8CEAB4C05EC",
        "mi": "11831",
        "url": "http://staging-media.ucic.vc/media/4F211D7B-5DA4-42FA-9C44-E8CEAB4C05EC/original.jpg",
        "display": "http://staging-media.ucic.vc/media/4F211D7B-5DA4-42FA-9C44-E8CEAB4C05EC/display.jpg",
        "thumb": "http://staging-media.ucic.vc/media/4F211D7B-5DA4-42FA-9C44-E8CEAB4C05EC/thumb.jpg",
        "lat": 43.4513854980469,
        "lon": -80.498664855957,
        "mimeType": "image/jpeg",
        "likes": 28,
        "badge": "https://media.ucic.vc/assets/tags/RU.png",
        "liked": false,
        "createdAt": "2016-04-22T01:29:37.000Z",
        "metaData": {
          "city": "Mozhaysk",
          "region": "Moskovskaya oblast'",
          "country": "Russia",
          "uploaded": 0,
          "createdAt": "2017-01-25T12:00:00.000Z",
          "location": {
            "lat": 47.45,
            "lon": 6.93546
          }
        },
        "tags": [
          {
            "id": "E73CD7C4-35E7-4A37-9850-950E22B2BCCF",
            "category": "country",
            "name": "United States of America"
          },
          {
            "id": "F8E5FF35-3CAD-462C-B115-3E0D0B0DF4D7",
            "category": "vision",
            "name": "spaniel"
          }
        ]
      }
    }
  }
]
```

This endpoint retrieves the cards for a specified request..

### HTTP Request

`GET https://node.ucic.vc/api/v04/requests/<ID>/cards`

### URL Parameters

| Parameter | Type    | Description                              |
| --------- | ------- | ---------------------------------------- |
| ID        | Integer | The ID of the Request to retrieve cards for |

### Query Parameters

| Parameter | Type             | Description                              |
| --------- | ---------------- | ---------------------------------------- |
| limit     | Unsigned Integer | Maximum number of cards to return        |
| offset    | Unsigned Integer | Offset in list of cards to start return from |
| page      | Unsigned Integer | Page of cards to return (note: overrides offset value if both are sent) |

## Get the Cards for a Question 

```shell
curl "https://node.ucic.vc/api/v04/questions/a29c2a61-7fee-492e-80e6-907c859b4419/cards" -H "Authorization: <AUTHORIZATION_TOKEN>"
```

```javascript

```

> The above command returns JSON structured like this:

```json
[
  {
    "id": "4F211D7B-5DA4-42FA-9C44-E8CEAB4C05EC",
    "tagId": "928CF4AC-A5BF-4A8B-8C47-62E58AE1F655",
    "comments": [{
      "id": "a8c1236a-5ab1-4874-b25e-3aeebdc15909",
      "text": "This is a comment ",
      "itemId": "4F211D7B-5DA4-42FA-9C44-E8CEAB4C05EC",
      "itemType": "card",
      "likeCount": 7,
      "liked": true,
      "createdAt": "2017-06-09 19:47:43",
      "creator": {
        "UI": "195502",
        "avatar": "https://media.ucic.vc/media/7C21E547-277A-4A23-934A-E7986B82E5EB/micro.jpg",
        "Username": "Jay Jay",
        "badge": "https://media.ucic.vc/assets/tags/CA.png"
      }
    }],
    "request": {
      "id": "40839",
      "body": "Anything interesting to see around you?",
      "createdAt": "2016-04-22T01:02:37.000Z",
      "requestType": 0,   // 0 = map, 1 = direct, 2 = global, 3 = event
      "likeCount": 7,
      "liked": false,
      "following": true,
      "sender": {
        "id": "36001",
        "fullname": "Jack Liu",
        "badge": "https://media.ucic.vc/assets/tags/CA.png",
        "avatar": "http://staging-media.ucic.vc/media/default/thumb.png"
      }
    },
    "response": {
      "id": "14062",
      "body": "Mural",
      "createdAt": "2016-04-22T01:29:23.530Z",
      "sender": {
        "id": "71",
        "fullname": "Ashley",
        "badge": "https://media.ucic.vc/assets/tags/CA.png",
        "avatar": "http://staging-media.ucic.vc/media/default/thumb.png"
      },
      "media": {
        "id": "4F211D7B-5DA4-42FA-9C44-E8CEAB4C05EC",
        "mi": "11831",
        "url": "http://staging-media.ucic.vc/media/4F211D7B-5DA4-42FA-9C44-E8CEAB4C05EC/original.jpg",
        "display": "http://staging-media.ucic.vc/media/4F211D7B-5DA4-42FA-9C44-E8CEAB4C05EC/display.jpg",
        "thumb": "http://staging-media.ucic.vc/media/4F211D7B-5DA4-42FA-9C44-E8CEAB4C05EC/thumb.jpg",
        "lat": 43.4513854980469,
        "lon": -80.498664855957,
        "mimeType": "image/jpeg",
        "likes": 28,
        "badge": "https://media.ucic.vc/assets/tags/RU.png",
        "liked": false,
        "createdAt": "2016-04-22T01:29:37.000Z",
        "metaData": {
          "city": "Mozhaysk",
          "region": "Moskovskaya oblast'",
          "country": "Russia",
          "uploaded": 0,
          "createdAt": "2017-01-25T12:00:00.000Z",
          "location": {
            "lat": 47.45,
            "lon": 6.93546
          }
        },
        "tags": [
          {
            "id": "E73CD7C4-35E7-4A37-9850-950E22B2BCCF",
            "category": "country",
            "name": "United States of America"
          },
          {
            "id": "F8E5FF35-3CAD-462C-B115-3E0D0B0DF4D7",
            "category": "vision",
            "name": "spaniel"
          }
        ]
      }
    }
  }
]
```

This endpoint retrieves the cards for a specified question..

### HTTP Request

`GET https://node.ucic.vc/api/v04/questions/<ID>/cards`

### URL Parameters

| Parameter | Type   | Description                              |
| --------- | ------ | ---------------------------------------- |
| ID        | String | The ID of the Question to retrieve cards for |

### Query Parameters

| Parameter | Type                                     | Description                              |
| --------- | ---------------------------------------- | ---------------------------------------- |
| limit     | Unsigned Integer                         | Maximum number of cards to return        |
| offset    | Unsigned Integer                         | Offset in list of cards to start return from |
| page      | Unsigned Integer                         | Page of cards to return (note: overrides offset value if both are sent) |
| sort      | String<'latestLike:desc', 'mediaCreated'> | What sort to apply to the returned cards. Default is `mediaCreated` |


## Hide a Card

```shell
curl -X PUT -H "Authorization: <AUTHORIZATION_TOKEN>" "https://node.ucic.vc/api/v05/card/DEC604AC-C29F-4764-B9C6-2CEC7351ABB6/hide"
```
```javascript

```

> The above command returns No Content 204

This endpoint hides a user's card.  The user must be the author of the card to hide

### HTTP Request

`PUT https://node.ucic.vc/api/v05/cards/<ID>/hide`

### URL Parameters

| Parameter | Type | Description                |
| --------- | ---- | -------------------------- |
| ID        | UUID | The ID of the card to hide |

