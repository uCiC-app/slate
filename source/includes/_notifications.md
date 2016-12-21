# Notifications

Notifications are delivered via Firebase Cloud Messaging.  The notification format is largely constrained by legacy support purposes.

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

Parameter | Type | Description
--------- | ---- | -----------
alert | String | Display text with user question and request type
badge | String | Presently unused
ID    | String | Request identifier (currently integer)
type  | String | The type of notification, Request is type 0
video | String | The request format identifier. 0 is photo and 1 is video


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

Parameter | Type | Description
--------- | ---- | -----------
alert | String | Display text including username that sent the message 
badge | String | Presently unused
ID    | String | Conversation UUID
type  | String | The type of notification, Message is type 1
video | String | The request format identifier.  Unused for message


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

Parameter | Type | Description
--------- | ---- | -----------
alert | String | Display text including username and question (always denotes 'photo' for legacy purposes)
badge | String | Presently unused
ID    | String | Response identifier (currently integer) 
type  | String | The type of notification, Response is type 4
video | String | The request format identifier.  Photo is 0 and Video is 1 


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

Parameter | Type | Description
--------- | ---- | -----------
alert | String | Display text including username and media type
badge | String | Presently unused
ID    | String | Related media/card UUID
type  | String | The type of notification, Comment is type 11
video | String | The request format identifier.  Unused for comment 


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

Parameter | Type | Description
--------- | ---- | -----------
alert | String | Display text including username and media type
badge | String | Presently unused
ID    | String | Related media/card UUID
type  | String | The type of notification, Like is type 9
video | String | The request format identifier.  Unused for like 


