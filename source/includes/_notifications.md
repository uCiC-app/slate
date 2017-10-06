# Notifications

Notifications are delivered via Firebase Cloud Messaging.  The notification format is largely constrained by legacy support purposes.

## Mute Notifications for entity

```shell
curl "https://node.ucic.vc/api/v04/notification/mute/media/E5DBDEE9-B427-4A52-BEB3-538289E96544"  -H "Authorization: <AUTHORIZATION_TOKEN>"
```
```javascript

```

> The above command returns a 204 success code

Most notifications and alerts are generated for items that the user either owns or follows. Any that are followed may always be unfollowed to stop the creation of these alerts/PNs. However, there are some items that the user may own that can generate a theoretically unlimited number of alerts. This route allows the user to disable alerts and notifications for a specified item.

### HTTP Request

`GET https://node.ucic.vc/api/v04/notification/mute/:itemType/:itemId`

### URL parameters

| param    | type   | Description                              |
| -------- | ------ | ---------------------------------------- |
| itemType | String | The type of item to silence alerts for. Currently supports `media`, `comment`, `question` |
| itemId   | String | The id of the specific item of itemType type to silence alerts for. See the [Mutable Entites table](https://ucic-app.github.io/ucic-docs/#mutable-entities) table below. |

## Unmute Notifications for entity


```shell
curl "https://node.ucic.vc/api/v04/notification/unmute/media/E5DBDEE9-B427-4A52-BEB3-538289E96544"  -H "Authorization: <AUTHORIZATION_TOKEN>"
```
```javascript

```

> The above command returns a 204 success code

Undo the mute action of the route above.

### HTTP Request

`GET https://node.ucic.vc/api/v04/notification/unmute/:itemType/:itemId`

### URL parameters

| param    | type   | Description                              |
| -------- | ------ | ---------------------------------------- |
| itemType | String | The type of item to unsilence alerts for. Currently supports `media`, `comment`, `question` |
| itemId   | String | The id of the specific item of itemType type to unsilence alerts for. See the [Mutable Entites table](https://ucic-app.github.io/ucic-docs/#mutable-entities) below. |

### Mutable Entities
| Entity                            | itemType   | itemId                                   |
| --------------------------------- | ---------- | ---------------------------------------- |
| Event Room Media or Response      | `media`    | The non-MI id of the card or media. Ie. `card.id` or `cardId`. |
| **Root level** Event Room Comment | `comment`  | `comment.id`                             |
| Event Room Question               | `question` | The numeric `requestId` (root `.id` value in the context of a `type="question"` event room item) |


## Request

> Sample Payload

```json
{
  "data": {
      "alert": "Falak wants you to take a photo of \"Is it busy there now?\"",
      "badge": "0",
      "ID": "46445",
      "type": "0",
      "video": "0"
  }
}
```

This notification represents a user request for image/video.  It is sent to response candidates when a request is created.

### Notification Parameters

| Parameter | Type   | Description                              |
| --------- | ------ | ---------------------------------------- |
| alert     | String | Display text with user question and request type |
| badge     | String | Presently unused                         |
| ID        | String | Request identifier (currently integer)   |
| type      | String | The type of notification, Request is type 0 |
| video     | String | The request format identifier. 0 is photo and 1 is video |


## Message

> Sample Payload

```json
{
  "data": {
      "alert": "Guy Streetley  has sent you a message",
      "badge": "0",
      "ID": "EB57B50B-21D3-41AF-B1F3-8E3F8235AAB1",
      "type": "1",
      "video": "0"
  }
}
```

This notification represents an incoming message.  It is sent to the other participants in a conversation.

### Notification Parameters

| Parameter | Type   | Description                              |
| --------- | ------ | ---------------------------------------- |
| alert     | String | Display text including username that sent the message |
| badge     | String | Presently unused                         |
| ID        | String | Conversation UUID                        |
| type      | String | The type of notification, Message is type 1 |
| video     | String | The request format identifier.  Unused for message |


## Response 

> Sample Response

```json
{
  "data": {
    "alert": "Guy  has sent a photo of \"How's the sunset there?\"",
    "badge": "0",
    "ID": "16100",
    "type": "4",
    "video": "1"
  }
}
```

This notification represents an incoming response to a user's request.  It is sent to the requester.

### Notification Parameters

| Parameter | Type   | Description                              |
| --------- | ------ | ---------------------------------------- |
| alert     | String | Display text including username and question (always denotes 'photo' for legacy purposes) |
| badge     | String | Presently unused                         |
| ID        | String | Response identifier (currently integer)  |
| type      | String | The type of notification, Response is type 4 |
| video     | String | The request format identifier.  Photo is 0 and Video is 1 |


## Comment 

> Sample Response 

```json
{
  "data": {
    "alert": "Falak commented on your photo",
    "badge": "0",
    "ID": "C6214A68-055D-4D71-A5F4-29727B6A301D",
    "type": "11",
    "video": "0"
  }
}
```

This notification represents an incoming comment to a media item.  It is sent to the media creator as well as requester.

### Notification Parameters

| Parameter | Type   | Description                              |
| --------- | ------ | ---------------------------------------- |
| alert     | String | Display text including username and media type |
| badge     | String | Presently unused                         |
| ID        | String | Related media/card UUID                  |
| type      | String | The type of notification, Comment is type 11 |
| video     | String | The request format identifier.  Unused for comment |


## Like 

```json
{
  "data": {
    "alert": "Guy  likes your photo",
    "badge": "0",
    "ID": "317666D8-8113-4323-B2FA-C60CA9F4066E",
    "type": "9",
    "video": "0"
  }
}
```

This notification represents a like to a media item.  It is sent to the media creator as well as requester.

### Notification Parameters

| Parameter | Type   | Description                              |
| --------- | ------ | ---------------------------------------- |
| alert     | String | Display text including username and media type |
| badge     | String | Presently unused                         |
| ID        | String | Related media/card UUID                  |
| type      | String | The type of notification, Like is type 9 |
| video     | String | The request format identifier.  Unused for like |

## Response on followed Request 

```json
{
  "data": {
    "alert": "Name added a response to \"What's going on over there?\"",
    "badge": "0",
    "ID": "300101",
    "type": "14",
    "video": "0"
  }
}
```

This notification represents a response to a request that the receiver is following. 

### Notification Parameters

| Parameter | Type   | Description                              |
| --------- | ------ | ---------------------------------------- |
| alert     | String | Display text including username and request text |
| badge     | String | Presently unused                         |
| ID        | String | The id of the followed request           |
| type      | String | The type of notification, Response on followed request is 14 |
| video     | String | The request format identifier.  Unused for this PN |


## Response on Event Room Question

```json
{
  "data": {
    "alert": "Name responded to your question \"What's going on over there?\"",
    "type": "20",
    "video": "0",
    "eventTitle": "The Best Test Event",
    "eventId": "1234567890",
    "itemType": "response",
    "itemId": "ca7b06cf-8604-4526-9397-41d461f96592"
  }
}
```

This notification represents a response to a request that the user created in an event room.

### Notification Parameters

| Parameter  | Type   | Description                              |
| ---------- | ------ | ---------------------------------------- |
| alert      | String | Display text including username and request text |
| type       | String | The type of notification, Response on event room question is 20 |
| video      | String | 1 if response is video                   |
| eventTitle | String | The name of the event the notification's action took place in |
| eventId    | String | The id of the event the notification's action took place in |
| itemType   | String | The `type` of the root event room item the interaction took place with/on |
| itemId     | String | The `id` of the root event room item the interaction took place with/on |

## Comment on Event Room Item

```json
{
  "data": {
    "alert": "Name commented on your {photo/video/comment}",
    "type": "21",
    "video": "0",
    "eventTitle": "The Best Test Event",
    "eventId": "1234567890",
    "itemType": "response",
    "itemId": "ca7b06cf-8604-4526-9397-41d461f96592"
  }
}
```

This notification represents receiving the first comment on a root level event room item.

### Notification Parameters

| Parameter  | Type   | Description                              |
| ---------- | ------ | ---------------------------------------- |
| alert      | String | Display text including username and request text |
| type       | String | The type of notification, this one uses 21 |
| video      | String | 1 if the root item is a video            |
| eventTitle | String | The name of the event the notification's action took place in |
| eventId    | String | The id of the event the notification's action took place in |
| itemType   | String | The `type` of the root event room item the interaction took place with/on |
| itemId     | String | The `id` of the root event room item the interaction took place with/on |

## Event Room Item Follow On Comment

```json
{
  "data": {
    "alert": "Name also commented on the {photo/video/comment}",
    "type": "22",
    "video": "0",
    "eventTitle": "The Best Test Event",
    "eventId": "1234567890",
    "itemType": "response",
    "itemId": "ca7b06cf-8604-4526-9397-41d461f96592"
  }
}
```

This notification represents someone commenting on an event room item after you have. You are only alerted with a PN for the first comment after your own.

### Notification Parameters

| Parameter  | Type   | Description                              |
| ---------- | ------ | ---------------------------------------- |
| alert      | String | Display text including username and request text |
| type       | String | The type of notification, this one uses 22 |
| video      | String | 1 if the root item is a video            |
| eventTitle | String | The name of the event the notification's action took place in |
| eventId    | String | The id of the event the notification's action took place in |
| itemType   | String | The `type` of the root event room item the interaction took place with/on |
| itemId     | String | The `id` of the root event room item the interaction took place with/on |

## New Followed Event Content

```json
{
  "data": {
    "alert": "Name added a {photo/video/comment} to an event you follow",
    "type": "23",
    "video": "0",
    "eventTitle": "The Best Test Event",
    "eventId": "1234567890",
    "itemType": "response",
    "itemId": "ca7b06cf-8604-4526-9397-41d461f96592"
  }
}
```

This notification represents someone adding a root level item to an event you follow. Note: this PN has a 3 hour cooldown. Alerts for the alert tab are still created during the cooldown without the push notification.

### Notification Parameters

| Parameter  | Type   | Description                              |
| ---------- | ------ | ---------------------------------------- |
| alert      | String | Display text including username and request text |
| type       | String | The type of notification, this one uses 23 |
| video      | String | 1 if the root item is a video            |
| eventTitle | String | The name of the event the notification's action took place in |
| eventId    | String | The id of the event the notification's action took place in |
| itemType   | String | The `type` of the root event room item the interaction took place with/on |
| itemId     | String | The `id` of the root event room item the interaction took place with/on |

## New Followed User Event Content

```json
{
  "data": {
    "alert": "Name added a {photo/video}",
    "type": "24",
    "video": "0",
    "eventTitle": "The Best Test Event",
    "eventId": "1234567890",
    "itemType": "response",
    "itemId": "ca7b06cf-8604-4526-9397-41d461f96592"
  }
}
```

This notification represents a user you follow adding a piece of media to an event room. Note: this PN has a 24 hour cooldown. Alerts for the alert tab are still created during the cooldown without the push notification.

### Notification Parameters

| Parameter  | Type   | Description                              |
| ---------- | ------ | ---------------------------------------- |
| alert      | String | Display text including username and request text |
| type       | String | The type of notification, this one uses 24 |
| video      | String | 1 if the root item is a video            |
| eventTitle | String | The name of the event the notification's action took place in |
| eventId    | String | The id of the event the notification's action took place in |
| itemType   | String | The `type` of the root event room item the interaction took place with/on |
| itemId     | String | The `id` of the root event room item the interaction took place with/on |

## Event Request Received

```json
{
  "data": {
    "alert": "Name asked a question about \"The Best Test Event\"",
    "type": "25",
    "eventTitle": "The Best Test Event",
    "eventId": "1234567890",
    "itemType": "question",
    "itemId": "300767"
  }
}
```

This notification represents a user asking a question to an event that you are either at or very close to (500m grace are on top of the event radius). 

### Notification Parameters

| Parameter  | Type   | Description                              |
| ---------- | ------ | ---------------------------------------- |
| alert      | String | Display text including username and request text |
| type       | String | The type of notification, this one uses 25 |
| eventTitle | String | The name of the event the notification's action took place in |
| eventId    | String | The id of the event the notification's action took place in |
| itemType   | String | The `type` of the root event room item the interaction took place with/on. Always `"question"` for this PN type |
| itemId     | String | The `id` of the root event room item the interaction took place with/on |