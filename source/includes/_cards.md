#Cards 

## Get a Specific Card 

```shell
curl "https://node.ucic.vc/api/v05/cards/DEC604AC-C29F-4764-B9C6-2CEC7351ABB6"
  -H "Authorization: <AUTHORIZATION_TOKEN>"
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

## Get the Comments for a Specific Card

```shell
```
```javascript
```

> The above command returns JSON structured like this:

```json
[
  {
    "id": "7CFFE67B-D74A-4EBC-9D0B-04AA18F540B1",
    "text": "Adding a comment to a card",
    "itemId": "DEC604AC-C29F-4764-B9C6-2CEC7351ABB6",
    "itemType": "card",
    "createdAt": "2016-12-18T22:18:04.000Z",
    "creator": {
      "UI": "611",
      "avatar": "http://staging-media.ucic.vc/media/8D33E7DA-D1FC-4DA4-B787-987916062D6D/thumb.png",
      "Username": "John Doe",
      "email": "z@z.com",
      "rating": 4,
      "createdAt": "2015-01-19T12:06:48.363Z"
    }
  }
]
```

This endpoint retrieves the comments for a card.

### HTTP Request

`GET https://node.ucic.vc/api/v05/cards/<ID>/comments`

### URL Parameters

Parameter | Type | Description
ID | UUID | The ID of the card to retrieve comments for

