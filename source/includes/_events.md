# Events 

## Get the Current User's Events

```shell

curl "https://node.ucic.vc/api/v04/events" -H "Authorization: <AUTHORIZATION_TOKEN>"
```

```javascript
```

> The above command returns JSON structured like this:

```json
[
  {
    "category": "response",
    "kind": "send",
    "content": {
      "sender": 38890,
      "receiver": "38988",
      "mimeType": "image/png",
      "url": "http://staging-media.ucic.vc/media/C6214A68-055D-4D71-A5F4-29727B6A301D/original.png"
    },
    "thumb": "http://staging-media.ucic.vc/media/C6214A68-055D-4D71-A5F4-29727B6A301D/thumb.png",
    "refId": "16087",
    "createdAt": "2016-12-18T15:41:13.000Z",
    "card": "https://node.ucic.vc/api/v05/card/C6214A68-055D-4D71-A5F4-29727B6A301D",
    "creator": {
      "UI": "38890",
      "Username": "Guy Streetley ",
      "Karma": "101",
      "email": "guy.streetley@gmail.com",
      "rating": 5,
      "createdAt": "2016-10-25T01:46:44.133Z",
      "avatar": "http://staging-media.ucic.vc/media/18B050D2-D4A4-49B8-9D0C-D92DC9FAFC32/thumb.png"
    }
  }
]
```

This endpoint retrieves the current user's events.

### HTTP Request

`GET https://node.ucic.vc/api/v04/events`

### Query Parameters

Parameter | Type | Description
--------- | ---- | -----------
limit | Unsigned Integer | Maximum number of comments to return
offset | Unsigned Integer | Offset in list of commentss to start return from
page | Unsigned Integer | Page of comments to return

## Update a user's event's seen status

```shell
curl -X PUT -H "Authorization: <AUTHORIZATION_TOKEN>" -H "Content-Type: application/json" -d '{ "seen": true }' "https://node.ucic.vc/api/v04/events/DEC604AC-C29F-4764-B9C6-2CEC7351ABB6" 
```

```javascript
```

> The above command returns 204 on success:

This endpoint update's the current user's event's status.

### HTTP Request

`PUT https://node.ucic.vc/api/v04/events/<ID>`

### Body Parameters

Parameter | Type | Description
--------- | ---- | -----------
seen | Boolean | Seen status of event

