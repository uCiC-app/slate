# Entities 


## Card

> Sample Payload

```json
```

Cards are a 1:1 media item relationship with related data.

### Card Entity Data Structure

Parameter | Type | Description
--------- | ---- | -----------


## Comment

> Sample Payload

```json
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
```

Comments represent a comment along with the associated creator user;

Parameter | Type | Description
--------- | ---- | -----------
id | UUID | Comment reference UUID
text | String | Content of comment
itemId | String | Associated item id of comment (Today only a Media/card reference)
itemType | String | Today only 'card'
createdAt | DateTime | Creation date of comment
creator | User | User who created the comment


## Conversation

> Sample Payload

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

Conversation is a list of chat thread participants with some useful metadata

Parameter | Type | Description
--------- | ---- | -----------
id | UUID | Conversation reference UUID
createdAt | DateTime | Conversation created date
lastMessage | String | The last Content sent in a conversation
lastMessageDate | DateTime | When the last Content sent in a conversation was sent
title | String | Currently unused
seen | Boolean | Whether a seen update has been sent for your user since the last message in the conversation
participants | [User] | User array of participants excluding the current user


## Map 

> Sample Payload

## Theme

> Sample Payload

```json
{
  "id": "E73CD7C4-35E7-4A37-9850-950E22B2BCCF",
  "name": "United States of America",
  "maxLikes": 78,
  "logo": "http://staging-media.ucic.vc/assets/tags/US.png"
}
```

A theme is a tag that can be applied to Media/Card items

Parameter | Type | Description
--------- | ---- | -----------
id | UUID | Theme tag ID
name | String | Name of tag
maxLikes | Integer | The maximum number of likes attributed to Media/Card with this theme
logo | HTTP URI | URL to the tag's logo


## User


