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


## EventQuestionResponse (20)

> Sample Payload

```json
{
  "data": {
    "eventTitle": "The Best Test Event",
    "eventId": "1234567890",
    "itemType": "response",
    "itemId": "E2E79146-4FD1-4835-BA76-B83E7291A373",
    "type": "20"
  }
}
```

This notification represents a user responding to a request created by the client user.  

### Notification Parameters

| Parameter  | Type   | Description                              |
| ---------- | ------ | ---------------------------------------- |
| eventTitle | String | Title of event the interaction took place in |
| eventId    | String | ID of event the interaction took place in |
| itemType   | String | The type of the root event room item the interaction took place in |
| itemId     | String | The ID of the root event room item the interaction took place in |
| type       | String | The PN type. EventQuestionResponse is 20 |

## EventItemComment (21)

> Sample Payload

```json
{
 "data": {
   "eventTitle": "The Best Test Event",
   "eventId": "1234567890",
   "itemType": "media",
   "itemId": "E2E79146-4FD1-4835-BA76-B83E7291A373",
   "type": "21"
  }
}
```

This notification represents someone having commented on a piece of media created by the client user.

### Notification Parameters

| Parameter  | Type   | Description                              |
| ---------- | ------ | ---------------------------------------- |
| eventTitle | String | Title of event the interaction took place in |
| eventId    | String | ID of event the interaction took place in |
| itemType   | String | The type of the root event room item the interaction took place in |
| itemId     | String | The ID of the root event room item the interaction took place in |
| type       | String | The PN type. EventItemComment is 21      |


## EventItemFollowOnComment (22) 

> Sample Response

```json
{
 "data": {
   "eventTitle": "The Best Test Event",
   "eventId": "1234567890",
   "itemType": "media",
   "itemId": "E2E79146-4FD1-4835-BA76-B83E7291A373",
   "type": "22"
  }
}
```

This notification represents someone having commented on an event room item after you commented on it last. 

### Notification Parameters

| Parameter  | Type   | Description                              |
| ---------- | ------ | ---------------------------------------- |
| eventTitle | String | Title of event the interaction took place in |
| eventId    | String | ID of event the interaction took place in |
| itemType   | String | The type of the root event room item the interaction took place in |
| itemId     | String | The ID of the root event room item the interaction took place in |
| type       | String | The PN type. EventItemFollowOnComment is 22 |


## FollowedEventContent (23) 

> Sample Response 

```json
{
 "data": {
   "eventTitle": "The Best Test Event",
   "eventId": "1234567890",
   "itemType": "media",
   "itemId": "E2E79146-4FD1-4835-BA76-B83E7291A373",
   "type": "23"
  }
}
```

This notification represents someone having submitted a new piece of content to an event room that the client user follows.

### Notification Parameters

| Parameter  | Type   | Description                              |
| ---------- | ------ | ---------------------------------------- |
| eventTitle | String | Title of event the interaction took place in |
| eventId    | String | ID of event the interaction took place in |
| itemType   | String | The type of the root event room item the interaction took place in |
| itemId     | String | The ID of the root event room item the interaction took place in |
| type       | String | The PN type. FollowedEventContent is 23  |


## EventRequestReceived (25) 

```json
{
 "data": {
   "eventTitle": "The Best Test Event",
   "eventId": "1234567890",
   "itemType": "question",
   "itemId": "300877",
   "type": "25"
  }
}
```

This notification represents a user having asked a new question to an event that the client user is currently within the bounds of.

### Notification Parameters

| Parameter  | Type   | Description                              |
| ---------- | ------ | ---------------------------------------- |
| eventTitle | String | Title of event the interaction took place in |
| eventId    | String | ID of event the interaction took place in |
| itemType   | String | The type of the root event room item the interaction took place in |
| itemId     | String | The ID of the root event room item the interaction took place in |
| type       | String | The PN type. EventRequestReceived is 25  |

## MissedInteractionsBundle (26)

```json
{
 "data": {
   "type": "26"
  }
}
```

This notification represents a user having accumulated a significant number of unseen "you" category Alerts without having received a push notification for a specified period of time.

### Notification Parameters

| Parameter | Type   | Description                              |
| --------- | ------ | ---------------------------------------- |
| type      | String | The PN type. MissedInteractionsBundle is 26 |

## MissedFollowedEventBundle (27)

```json
{
 "data": {
   "type": "27"
  }
}
```

This notification represents a user having accumulated a significant number of unseen "followedEvent" category Alerts without having received a push notification for a specified period of time.

### Notification Parameters

| Parameter | Type   | Description                              |
| --------- | ------ | ---------------------------------------- |
| type      | String | The PN type. MissedFollowedEventBundle is 27 |

## MissedFollowedUserBundle (28)

```json
{
 "data": {
   "type": "28"
  }
}
```

This notification represents a user having accumulated a significant number of unseen "followedUser" category Alerts without having received a push notification for a specified period of time.

### Notification Parameters

| Parameter | Type   | Description                              |
| --------- | ------ | ---------------------------------------- |
| type      | String | The PN type. MissedFollowedUserBundle is 28 |

## BreakingNewsGlobal (29) 

```json
{
 "data": {
   "eventTitle": "The Best Test Event",
   "eventId": "1234567890",
   "type": "29"
  }
}
```

This notification represents a significant event occuring somewhere on the planet in one of the client user's subscribed subcategories.

### Notification Parameters

| Parameter  | Type   | Description                           |
| ---------- | ------ | ------------------------------------- |
| eventTitle | String | Title of event the event              |
| eventId    | String | ID of the event                       |
| type       | String | The PN type. BreakingNewsGlobal is 29 |

## BreakingNewsLocal (30) 

```json
{
 "data": {
   "eventTitle": "The Best Test Event",
   "eventId": "1234567890",
   "type": "30"
  }
}
```

This notification represents a significant event occuring at the client user's location.

### Notification Parameters

| Parameter  | Type   | Description                          |
| ---------- | ------ | ------------------------------------ |
| eventTitle | String | Title of event the event             |
| eventId    | String | ID of the event                      |
| type       | String | The PN type. BreakingNewsLocal is 30 |

## LocalEventStart (31) 

```json
{
 "data": {
   "eventTitle": "The Best Test Event",
   "eventId": "1234567890",
   "type": "30"
  }
}
```

This notification represents an event starting up at the user's location.

### Notification Parameters

| Parameter  | Type   | Description                          |
| ---------- | ------ | ------------------------------------ |
| eventTitle | String | Title of event the event             |
| eventId    | String | ID of the event                      |
| type       | String | The PN type. BreakingNewsLocal is 30 |

## BestRecentMedia (32) 

```json
{
 "data": {
   "eventTitle": "The Best Test Event",
   "eventId": "1234567890",
   "itemType": "media",
   "itemId": "E2E79146-4FD1-4835-BA76-B83E7291A373",
   "type": "32"
  }
}
```

This periodic notification highlights the most liked piece of media in the platform from the last week.

### Notification Parameters

| Parameter  | Type   | Description                              |
| ---------- | ------ | ---------------------------------------- |
| eventTitle | String | Title of event media was submitted to    |
| eventId    | String | ID of event the media was submitted to   |
| itemType   | String | The type of the item that is the top media |
| itemId     | String | The ID of the item that is the top media |
| type       | String | The PN type. BestRecentMedia is 32       |

## TrophyEarned (33) 

```json
{
 "data": {
   "name": "Quality Photographer",
   "trophyType": "photoLikes",
   "tier": 2,
   "type": 33
  }
}
```

This periodic notification highlights the most liked piece of media in the platform from the last week.

### Notification Parameters

| Parameter  | Type    | Description                         |
| ---------- | ------- | ----------------------------------- |
| name       | String  | The readable name of the trophy     |
| trophyType | String  | The coded identifier for the trophy |
| tier       | Integer | The tier of the earned trophy       |
| type       | String  | The PN type. TrophyEarned is 33     |