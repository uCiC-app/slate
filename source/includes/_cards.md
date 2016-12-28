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
    "request": {
      "id": "40839",
      "createdAt": "2016-04-22T01:02:37.000Z",
      "sender": {
        "id": "36001",
        "login": null,
        "fullname": "Jack Liu",
        "email": "jackjack_liu@hotmail.com",
        "avatar": "http://staging-media.ucic.vc/media/default/thumb.png",
        "lat": 48.715,
        "lon": -80.5174639,
        "likes": "10",
        "createdAt": "2016-04-22T01:01:54.446Z"
      },
      "receiver": null,
      "body": "Anything interesting to see around you?",
      "media": null
    },
    "response": {
      "id": "14062",
      "createdAt": "2016-04-22T01:29:23.530Z",
      "sender": {
        "id": "71",
        "login": "uCiC_app",
        "fullname": "Ashley",
        "email": "",
        "avatar": "http://staging-media.ucic.vc/media/default/thumb.png",
        "likes": "10",
        "responses": 84,
        "createdAt": "2014-08-31T18:44:51.156Z"
      },
      "receiver": null,
      "body": "Mural",
      "media": {
        "id": "4F211D7B-5DA4-42FA-9C44-E8CEAB4C05EC",
        "mi": "11831",
        "url": "http://staging-media.ucic.vc/media/4F211D7B-5DA4-42FA-9C44-E8CEAB4C05EC/original.jpg",
        "thumb": "http://staging-media.ucic.vc/media/4F211D7B-5DA4-42FA-9C44-E8CEAB4C05EC/thumb.jpg",
        "lat": 43.4513854980469,
        "lon": -80.498664855957,
        "mimeType": "image/jpeg",
        "likes": 28,
        "liked": false,
        "createdAt": "2016-04-22T01:29:37.000Z",
        "tags": []
      }
    }
  }
]
```

This endpoint retrieves the cards for a theme.

### HTTP Request

`GET https://node.ucic.vc/api/v05/themes/<ID>/cards`

### URL Parameters

Parameter | Type | Description
--------- | ---- | -----------
ID | UUID | The ID of the theme to retrieve cards for

### Query Parameters

Parameter | Type | Description
--------- | ------- | -----------
limit | Unsigned Integer | Maximum number of cards to return
offset | Unsigned Integer | Offset in list of cards to start return from
page | Unsigned Integer | Page of cards to return
sort | String | Sort by 'createdAt' or likes'.  Default is 'likes'
order | String | Direction of sort, either 'ASC' for ascending or 'DESC' for descending, default is DESC 

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
  "request": {
    "id": "46154",
    "createdAt": "2016-12-09T22:40:22.100Z",
    "sender": {
      "id": "38988",
      "login": null,
      "fullname": "Falak",
      "email": "a@b.com",
      "avatar": "http://staging-media.ucic.vc/media/default/thumb.png",
      "lat": 43.4509175,
      "lon": -80.498604,
      "likes": "0",
      "createdAt": "2016-11-05T05:43:08.916Z"
    },
    "receiver": null,
    "body": "How's the sunset there?",
    "media": null
  },
  "response": {
    "id": "15958",
    "createdAt": "2016-12-09T22:40:22.100Z",
    "sender": {
      "id": "39124",
      "login": null,
      "fullname": "Gbs",
      "email": "guy@gmail.com",
      "avatar": "http://staging-media.ucic.vc/media/default/thumb.png",
      "likes": "0",
      "responses": 2,
      "createdAt": "2016-12-09T19:00:53.233Z"
    },
    "receiver": null,
    "body": "",
    "media": {
      "id": "F48F16C0-81BE-418D-B44B-9F97DD2D3A70",
      "mi": "13370",
      "url": "http://staging-media.ucic.vc/media/F48F16C0-81BE-418D-B44B-9F97DD2D3A70/original.png",
      "thumb": "http://staging-media.ucic.vc/media/F48F16C0-81BE-418D-B44B-9F97DD2D3A70/thumb.png",
      "lat": 43.4531783,
      "lon": -80.495723,
      "mimeType": "image/png",
      "likes": 10,
      "liked": false,
      "createdAt": "2016-12-10T01:58:01.653Z",
      "tags": []
    }
  }
}
```

This endpoint retrieves a specific card.

### HTTP Request

`GET https://node.ucic.vc/api/v05/cards/<ID>`

### URL Parameters

Parameter | Type | Description
--------- | ---- | -----------
ID | UUID | The ID of the card to retrieve


## Get User's Requested Cards

```shell
curl "https://node.ucic.vc/api/v04/users/requests" -H "Authorization: <AUTHORIZATION_TOKEN>"
```

```javascript
```

> The above command returns JSON structured like this:

```json
[
  {
    "id": "88F95DFB-0080-40F1-9529-55FBB74FC55D",
    "tagId": "928CF4AC-A5BF-4A8B-8C47-62E58AE1F655",
    "request": {
      "id": "45691",
      "createdAt": "2016-11-28T18:15:15.166Z",
      "sender": {
        "id": "611",
        "login": "z",
        "fullname": "John Doe",
        "email": "z@z.com",
        "avatar": "http://staging-media.ucic.vc/media/default/thumb.png",
        "lat": -22.9035393,
        "lon": -43.2095869,
        "likes": "10",
        "createdAt": "2015-01-19T12:06:48.363Z"
      },
      "receiver": null,
      "body": "How is the beach there?",
      "media": null
    },
    "response": {
      "id": "15790",
      "createdAt": "2016-11-28T18:15:15.166Z",
      "sender": {
        "id": "39086",
        "login": null,
        "fullname": "yhhji",
        "email": "hgdf@hjjh.bh",
        "avatar": "http://staging-media.ucic.vc/media/default/thumb.png",
        "likes": "0",
        "responses": 1,
        "createdAt": "2016-11-30T00:53:19.180Z"
      },
      "receiver": null,
      "body": "for",
      "media": {
        "id": "88F95DFB-0080-40F1-9529-55FBB74FC55D",
        "mi": "13254",
        "url": "http://staging-media.ucic.vc/media/88F95DFB-0080-40F1-9529-55FBB74FC55D/original.jpg",
        "thumb": "http://staging-media.ucic.vc/media/88F95DFB-0080-40F1-9529-55FBB74FC55D/thumb.jpg",
        "lat": 43.45162600766234,
        "lon": -80.4984725455851,
        "mimeType": "image/jpeg",
        "likes": 10,
        "liked": false,
        "createdAt": "2016-11-30T00:57:14.213Z",
        "tags": []
      }
    }
  }
]
```

This endpoint retrieves the cards that a user has requested.

### HTTP Request

`GET https://node.ucic.vc/api/v04/users/requests`

### Query Parameters

Parameter | Type | Description
--------- | ---- | -----------
limit | Unsigned Integer | Maximum number of comments to return
offset | Unsigned Integer | Offset in list of commentss to start return from
page | Unsigned Integer | Page of comments to return
sort | String | Sort by 'createdAt' or likes'.  Default is 'likes'
order | String | Direction of sort, either 'ASC' for ascending or 'DESC' for descending, default is DESC 


## Get User's Responded Cards

```shell
curl "https://node.ucic.vc/api/v04/users/responses" -H "Authorization: <AUTHORIZATION_TOKEN>"
```

```javascript
```

> The above command returns JSON structured like this:

```json
[
  {
    "id": "08241390-F145-4245-A68A-5D7852488673",
    "tagId": "4F45AA05-0522-4674-8178-FE9983DE4BC4",
    "request": {
      "id": "45220",
      "createdAt": "2016-11-08T23:01:13.260Z",
      "sender": {
        "id": "38992",
        "login": null,
        "fullname": "duty3test",
        "email": "duty3@test.com",
        "avatar": "http://staging-media.ucic.vc/media/default/thumb.png",
        "lat": 33.2156041,
        "lon": -96.7934718,
        "likes": "0",
        "createdAt": "2016-11-07T19:42:06.203Z"
      },
      "receiver": null,
      "body": "Are you close to the beach? Can you show me a photo?",
      "media": null
    },
    "response": {
      "id": "15957",
      "createdAt": "2016-11-08T23:01:13.260Z",
      "sender": {
        "id": "611",
        "login": "z",
        "fullname": "John Doe",
        "email": "z@z.com",
        "avatar": "http://staging-media.ucic.vc/media/default/thumb.png",
        "likes": "10",
        "responses": 14,
        "createdAt": "2015-01-19T12:06:48.363Z"
      },
      "receiver": null,
      "body": "Hi There!",
      "media": {
        "id": "08241390-F145-4245-A68A-5D7852488673",
        "mi": "13369",
        "url": "http://staging-media.ucic.vc/media/08241390-F145-4245-A68A-5D7852488673/original.mp4",
        "thumb": "http://staging-media.ucic.vc/media/2A6F06F8-6CCE-45AE-9920-D7F7D515E31B/thumb.png",
        "lat": -22.9035393,
        "lon": -43.2095869,
        "mimeType": "video/mp4",
        "likes": 10,
        "liked": true,
        "createdAt": "2016-12-09T19:50:12.830Z",
        "tags": []
      }
    }
  }
]
```

This endpoint retrieves the cards that the current user has responded to requests with.

### HTTP Request

`GET https://node.ucic.vc/api/v04/users/responses`

### Query Parameters

Parameter | Type | Description
--------- | ---- | -----------
limit | Unsigned Integer | Maximum number of comments to return
offset | Unsigned Integer | Offset in list of commentss to start return from
page | Unsigned Integer | Page of comments to return
sort | String | Sort by 'createdAt' or likes'.  Default is 'likes'
order | String | Direction of sort, either 'ASC' for ascending or 'DESC' for descending, default is DESC 


