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
      "caption": "The caption for the response in events pertaining to one.",
      "mimeType": "image/jpeg",
      "url": "https://media.ucic.vc/media/8602814D-0CE1-444D-95BF-824CD6CBF186/display.jpg"
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
      "avatar": "http://media.ucic.vc/media/AC725D7D-72C0-41D8-85E0-F602091420D7/thumb.jpg",
      "badge": "https://media.ucic.vc/assets/tags/CA.png"
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

### Events as of Event Room introduction

**Note:** Alerts that refer to an event room item will contain `itemType` and `itemId` which will always refer to the root level item in which the interaction took place for the purpose of retrieval of this item with the route [Get Single Event Room Item](https://ucic-app.github.io/ucic-docs/#get-single-event-room-item)

**Note 2:** In the event of an event room item alert that refers to an `extMedia` item specifically, any `content` that would normally contain a String `mimeType` fiield will instead contain a Boolean `video` field for the purpose of placing a "play" button overlay on the thumbnail. This is done because the mimetypes of external media are more diverse and not explicitly calculated. 

** Category: "followedUser"**
*Kind: "eventResponse"*
A user you follow added a response/piece of media to an event room.
> followedUser/eventResponse
```
...
content: {
  "eventTitle": "Permian Basin Fair & Exposition",
  "eventId": "Oa8w5r4rrXOZ",
  "itemId": "ACDDF71B-1E1E-4445-A0CC-943301479A92",
  "itemType": "response",
  "mimeType": "image/jpeg"
},
"thumb": "https://media.ucic.vc/media/ACDDF71B-1E1E-4445-A0CC-943301479A92/thumb.jpg",
...
```

*Kind: "eventItemComment"*
A user you follow added a comment to an event room item. Note: the `refId` is the specific comment the alert refers to.
> followedUser/eventItemComment
```
...
content: {
  "eventTitle": "Permian Basin Fair & Exposition",
  "eventId": "Oa8w5r4rrXOZ",
  "itemId": "ACDDF71B-1E1E-4445-A0CC-943301479A92",
  "itemType": "response",
  "mimeType": "image/jpeg"
},
"refId": "7804d8c9-9cbc-48c1-9007-43b16b99ec6f",
"thumb": "https://pbs.twimg.com/media/DKBLEh_VAAAqiXk.jpg",
...
```

*Kind: "rootEventComment"*
A user you follow added a root level comment to an event room. Note: the `refId` is the specific root level comment the alert refers to.

> followedUser/rootEventComment
```
...
content: {
  "eventTitle": "Permian Basin Fair & Exposition",
  "eventId": "Oa8w5r4rrXOZ"
},
"refId": "7804d8c9-9cbc-48c1-9007-43b16b99ec6f",
...
```

**Category: "followedEvent"**
*Kind: "response"*
A user added a response to an event room you follow. 
> followedEvent/response
```
...
"content": {
  "eventTitle": "Permian Basin Fair & Exposition",
  "eventId": "Oa8w5r4rrXOZ",
  "id": "5D74DD0A-3EA7-4F6C-A04A-6C5F8C9220C8",
  "type": "response",
  "mimeType": "image/jpeg"
},
"thumb": "https://media.ucic.vc/media/5D74DD0A-3EA7-4F6C-A04A-6C5F8C9220C8/thumb.jpg",
...
```
*Kind: "comment"*  

A user added a root level comment to an event you follow . Note: the `refId` is the specific root level comment the alert refers to.
> followedEvent/comment  

```
...
"content": {
  "eventTitle": "Permian Basin Fair & Exposition",
  "eventId": "Oa8w5r4rrXOZ",
  "id": "5D74DD0A-3EA7-4F6C-A04A-6C5F8C9220C8",
  "type": "response",
  "mimeType": "image/jpeg"
},
"thumb": "https://media.ucic.vc/media/5D74DD0A-3EA7-4F6C-A04A-6C5F8C9220C8/thumb.jpg",
"refId": "5D74DD0A-3EA7-4F6C-A04A-6C5F8C9220C8",
...
```
**Category: "eventRequest"**
*Kind: "response"*
A user added a response to an event room request you asked.
>eventRequest/response
```
...
"content": {
  "eventTitle": "Permian Basin Fair & Exposition",
  "eventId": "Oa8w5r4rrXOZ",
  "itemId": "94C547B4-C827-4D12-AC43-D05E2C723D18",
  "itemType": "response",
  "mimeType": "image/jpeg"
},
"thumb": "https://media.ucic.vc/media/94C547B4-C827-4D12-AC43-D05E2C723D18/thumb.jpg",
...
```

*Kind: "like"*
A user liked an event question you asked.
>eventRequest/like  

```
...
"content": {
  "eventTitle": "Permian Basin Fair & Exposition",
  "eventId": "Oa8w5r4rrXOZ",
  "itemType": "question",
  "itemId": "300763"
},
...
```
**Category: "eventItemComment"**
*Kind: "like"*
A user liked your comment on an event room item. Note: `refId` refers to the specific liked comment on the item. Note2: `mimeType` and `thumb` will not be present if the root level item is a comment. 
>eventItemComment/like
```
...
"content": {
  "eventTitle": "Permian Basin Fair & Exposition",
  "eventId": "Oa8w5r4rrXOZ",
  "itemType": "response",
  "itemId": "ACDDF71B-1E1E-4445-A0CC-943301479A92",
  "mimeType": "image/jpeg"
},
"thumb": "https://media.ucic.vc/media/ACDDF71B-1E1E-4445-A0CC-943301479A92/thumb.jpg",
...
```

*Kind: "followOnComment"*
A user commented on an event room item after you did.  Note: `refId` refers to the comment that was created after yours, thus creating this alert. Note2: `mimeType` and `thumb` will not be present if the root level item is a comment. 
>eventItemComment/followOnComment
```
...
"content": {
  "eventTitle": "Permian Basin Fair & Exposition",
  "eventId": "Oa8w5r4rrXOZ",
  "itemType": "response",
  "itemId": "ACDDF71B-1E1E-4445-A0CC-943301479A92",
  "mimeType": "image/jpeg"
},
"thumb": "https://media.ucic.vc/media/ACDDF71B-1E1E-4445-A0CC-943301479A92/thumb.jpg",
...
```

**Category: "eventResponse"**
*Kind: "comment"*
A user commented on a `response` or `media` item that you created. 
>eventResponse/comment
```
...
"content": {
  "eventTitle": "Permian Basin Fair & Exposition",
  "eventId": "Oa8w5r4rrXOZ",
  "itemType": "media",
  "itemId": "03BAE8F6-BE39-4913-A4B8-2D910C6F148A",
  "mimeType": "image/jpeg"
},
"thumb": "https://media.ucic.vc/media/03BAE8F6-BE39-4913-A4B8-2D910C6F148A/thumb.jpg",
...
```

*Kind: "like"*
A user liked a `response` or `media` item that you created. 
>eventResponse/like  

```
...
"content": {
  "eventTitle": "Permian Basin Fair & Exposition",
  "eventId": "Oa8w5r4rrXOZ",
  "itemType": "media",
  "itemId": "03BAE8F6-BE39-4913-A4B8-2D910C6F148A",
  "mimeType": "image/jpeg"
},
"thumb": "https://media.ucic.vc/media/03BAE8F6-BE39-4913-A4B8-2D910C6F148A/thumb.jpg",
...
```
**Category: "rootComment"**
*Kind: "reply"*
A user replied with a comment on a root level `comment` item that you created in an event room. Note: `refId` refers to the specific added comment on the item.
>rootComment/reply
```
...
"content": {
  "eventTitle": "Permian Basin Fair & Exposition",
  "eventId": "Oa8w5r4rrXOZ",
  "itemType": "comment",
  "itemId": "9e32a980-3f80-4d31-b941-d9dca21f8aba"
},
"refId": "88c61150-19b9-4450-9489-367d2a5a0d62",
...
```

*Kind: "like"*
A user liked a root level `comment` item that you created in an event room.
>rootComment/like
```
...
"content": {
  "eventTitle": "Permian Basin Fair & Exposition",
  "eventId": "Oa8w5r4rrXOZ",
  "itemType": "comment",
  "itemId": "9e32a980-3f80-4d31-b941-d9dca21f8aba"
},
...
```



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