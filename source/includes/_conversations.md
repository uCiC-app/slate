# Conversations 

## Get all of the current user's conversations 

```shell
curl "https://node.ucic.vc/api/v04/conversations" -H "Authorization: <AUTHORIZATION_TOKEN>"
```

```javascript
```

> The above command returns JSON structured like this:

```json
[
  {
    "id": "D524F62B-E0C6-43CC-86E6-464FEE903B24",
    "createdAt": "2016-12-15T23:07:44.000Z",
    "updatedAt": "2016-12-15T23:07:44.000Z",
    "lastMessage": "HELLO THERE!!!!",
    "lastMessageDate": "2016-12-15T23:07:44.056Z",
    "title": null,
    "seen": false,
    "participants": [
      {
        "UI": "611",
        "Username": "John Doe",
        "Karma": "110",
        "email": "z@z.com",
        "rating": 4,
        "createdAt": "2015-01-19T12:06:48.363Z",
        "avatar": "http://staging-media.ucic.vc/media/611/thumb.png",
        "located": {
          "Lat": -22.9035393,
          "Lon": -43.2095869
        }
      }
    ]
  }
]
```

This endpoint retrieves all of a user's conversations.

### HTTP Request

`GET https://node.ucic.vc/api/v05/conversations`

### Query Parameters

Parameter | Type | Description
--------- | ---- | -----------
limit | Unsigned Integer | Maximum number of themes to return
offset | Unsigned Integer | Offset in list of themes to start return from
page | Unsigned Integer | Page of themes to return


## Get a specific Conversation

```shell
curl "https://node.ucic.vc/api/v04/conversations/d524f62b-e0c6-43cc-86e6-464fee903b24" -H "Authorization: <AUTHORIZATION_TOKEN>"
```
```javascript
```

> The above command returns JSON structured like this:

```json
{
  "id": "D524F62B-E0C6-43CC-86E6-464FEE903B24",
  "createdAt": "2016-12-15T23:07:44.000Z",
  "updatedAt": "2016-12-15T23:07:44.000Z",
  "lastMessage": "HELLO THERE!!!!",
  "lastMessageDate": "2016-12-15T23:07:44.056Z",
  "title": null,
  "seen": false,
  "participants": [
    {
      "UI": "611",
      "Username": "John Doe",
      "Karma": "110",
      "email": "z@z.com",
      "rating": 4,
      "createdAt": "2015-01-19T12:06:48.363Z",
      "avatar": "http://staging-media.ucic.vc/media/611/thumb.png",
      "located": {
        "Lat": -22.9035393,
        "Lon": -43.2095869
      }
    }
  ]
}
```

This endpoint retrieves a conversation.   The current user must have access to this conversation.

### HTTP Request

`GET https://node.ucic.vc/api/v05/conversation/<ID>`

### URL Parameters

Parameter | Type | Description
--------- | ---- | -----------
ID | UUID | The ID of the conversation to retrieve


## Get the Messages for a Specific Conversation 

```shell
curl "https://node.ucic.vc/api/v04/conversation/d524f62b-e0c6-43cc-86e6-464fee903b24/messages" -H "Authorization: <AUTHORIZATION_TOKEN>"
```
```javascript
```

> The above command returns JSON structured like this:

```json
[
  {
    "MI": "16698",
    "Text": "Hello there!",
    "CreateDate": "2016-12-15T23:07:44.000Z",
    "sender": {
      "UI": "611",
      "Username": "John Doe",
      "Karma": "110",
      "email": "z@z.com",
      "rating": 4,
      "createdAt": "2015-01-19T12:06:48.363Z",
      "avatar": "http://staging-media.ucic.vc/media/8D33E7DA-D1FC-4DA4-B787-987916062D6D/thumb.png"
    }
  }
]
```

This endpoint retrieves the messages for a conversation.  The current user must
have access to this conversation.

### HTTP Request

`GET https://node.ucic.vc/api/v04/conversations/<ID>/messages`

### URL Parameters

Parameter | Type | Description
--------- | ---- | -----------
ID | UUID | The ID of the conversation to retrieve messages for

### Query Parameters

Parameter | Type | Description
--------- | ---- | -----------
limit | Unsigned Integer | Maximum number of comments to return
offset | Unsigned Integer | Offset in list of commentss to start return from
page | Unsigned Integer | Page of comments to return


