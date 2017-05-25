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
    "id": "31035070-7179-44AE-A142-90D4DEF16E24",
    "category": "message",
    "kind": "new",
    "content": {
      "sender": 176039,
      "receiver": "18",
      "id": "84780",
      "message": "for followed request response, this is the original request message"
    },
    "thumb": null,
    "refId": "84780",
    "createdAt": "2017-02-10T02:08:32.000Z",
    "card": "https://api3.ucic.vc/api/v04/conversation/085170C2-7A3A-4DF7-9AF4-6B889DDBF1B9",
    "creator": {
      "UI": "176039",
      "Username": "Guy Streetley",
      "Karma": "115",
      "email": "guy@gmail.com",
      "rating": 5,
      "createdAt": "2016-10-20T18:16:35.960Z",
      "avatar": "http://media.ucic.vc/media/AC725D7D-72C0-41D8-85E0-F602091420D7/thumb.jpg"
    },
    "seen": false
  }
]
```

This endpoint retrieves the current user's events.

### HTTP Request

`GET https://node.ucic.vc/api/v04/events`

### Query Parameters

| Parameter | Type             | Description                              |
| --------- | ---------------- | ---------------------------------------- |
| limit     | Unsigned Integer | Maximum number of comments to return     |
| offset    | Unsigned Integer | Offset in list of commentss to start return from |
| page      | Unsigned Integer | Page of comments to return               |

## Update a user's event's seen status

```shell
curl -X PUT -H "Authorization: <AUTHORIZATION_TOKEN>" -H "Content-Type: application/json" -d '{ "seen": true }' "https://node.ucic.vc/api/v04/events/DEC604AC-C29F-4764-B9C6-2CEC7351ABB6" 
```

```javascript

```

> The above command returns 204 on success

This endpoint updates the current user's event's status.

### HTTP Request

`PUT https://node.ucic.vc/api/v04/events/<ID>`

### Body Parameters

| Parameter | Type    | Description          |
| --------- | ------- | -------------------- |
| seen      | Boolean | Seen status of event |

## Update all user's events to seen

```shell
curl -X PUT -H "Authorization: <AUTHORIZATION_TOKEN>" -H "Content-Type: application/json" -d '{}' "https://node.ucic.vc/api/v04/events/bulkSeen" 
```
```javascript

```
> The above command returns 204 on success:

This endpoint marks all of the user's events as seen. No body parameters are necessary.

### HTTP Request

`PUT https://node.ucic.vc/api/v04/events/bulkSeen`