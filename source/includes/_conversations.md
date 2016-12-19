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
    "senderSeen": true,
    "receiverSeen": false,
    "lastMessage": "HELLO THERE!!!!",
    "lastMessageDate": "2016-12-15T23:07:44.056Z",
    "title": null,
    "sender": {
      "UI": "611",
      "Username": "John Doe",
      "Login": "z",
      "Email": "z@z.com",
      "Karma": "110",
      "Address": "z",
      "Fulfilled": "9",
      "Rating": 4,
      "Registered": "2015-01-19T12:06:48.363Z",
      "IsLocked": false,
      "avatar": "8D33E7DA-D1FC-4DA4-B787-987916062D6D"
    },
    "receiver": {
      "UI": "12340",
      "Username": "Hks Jklv",
      "Login": null,
      "Email": "husseinmajid1985@gmail.com",
      "Karma": "100",
      "Address": "",
      "Fulfilled": "0",
      "Rating": 5,
      "Registered": "2015-10-01T07:53:17.666Z",
      "IsLocked": false,
      "avatar": null
    }
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
  "senderSeen": true,
  "receiverSeen": false,
  "lastMessage": "HELLO THERE!!!!",
  "lastMessageDate": "2016-12-15T23:07:44.056Z",
  "title": null,
  "sender": {
    "UI": "611",
    "Username": "John Doe",
    "Login": "z",
    "Email": "z@z.com",
    "Karma": "110",
    "Address": "z",
    "Fulfilled": "9",
    "Rating": 4,
    "Registered": "2015-01-19T12:06:48.363Z",
    "IsLocked": false,
    "avatar": "8D33E7DA-D1FC-4DA4-B787-987916062D6D"
  },
  "receiver": {
    "UI": "12340",
    "Username": "Hks Jklv",
    "Login": null,
    "Email": "husseinmajid1985@gmail.com",
    "Karma": "100",
    "Address": "",
    "Fulfilled": "0",
    "Rating": 5,
    "Registered": "2015-10-01T07:53:17.666Z",
    "IsLocked": false,
    "avatar": null
  }
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
    "Text": "The first message in a conversation",
    "CreateDate": "2016-12-15T23:07:44.000Z",
    "sender": {
      "UI": "611",
      "Username": "John Doe",
      "Login": "z",
      "Email": "z@z.com",
      "Karma": "110",
      "Address": "z",
      "Fulfilled": "9",
      "Rating": 4,
      "Registered": "2015-01-19T12:06:48.363Z",
      "IsLocked": false
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


