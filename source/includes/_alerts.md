# Alerts 

Alerts are now broken down into 3 categories named `you`, `followedEvent`, and `followedUser`. 


## Get the Current User's Alerts

```shell

curl "https://node.ucic.vc/api/v04/alert/:category" -H "Authorization: <AUTHORIZATION_TOKEN>"
```

```javascript

```

> The above command returns JSON structured like this:

```json
[{
  "id": "1ea412d0-fa56-4a57-9dda-bab55d25b5ff",
  "type": "followedUserLikedQuestion",
  "date": "2017-11-01T20:27:01.000Z",
  "seen": true,
  "itemType": "question",
  "itemId": "301255",
  "data": {
    "eventTitle": "The Best Test Event ",
    "eventId": "1234567890",
    "user": {
      "userId": 227108,
      "userName": "Sir_issac",
      "avatar": null,
      "badge": "https://media.ucic.vc/assets/tags/DZ.png"
    },
    "question": {
      "RI": 301255,
      "text": "The 15th Best Test Question"
    }
  }
}]
```

This endpoint retrieves the current user's alerts of the type specified in the url parameters. The specific data structure varies between alerts and each type is broken down in the rest of this section.  
**Note:** All events of a given category are marked as seen after any number of events of that category are returned to the client.

### HTTP Request

`GET https://node.ucic.vc/api/v04/alert/:category`

### URL Parameters

| Parameter | Type   | Description                              |
| --------- | ------ | ---------------------------------------- |
| category  | String | One of `you`, `followedUser`, `followedEvent` |


### Query Parameters

| Parameter | Type             | Description                              |
| --------- | ---------------- | ---------------------------------------- |
| limit     | Unsigned Integer | Maximum number of alerts to return       |
| offset    | Unsigned Integer | Offset in list of alerts to start return from |

### Alerts as of Event Room introduction

**Note:** Alerts that refer to an event room item will contain `itemType` and `itemId` which will always refer to the root level item in which the interaction took place for the purpose of retrieval of this item with the route [Get Single Event Room Item](https://ucic-app.github.io/ucic-docs/#get-single-event-room-item)

##Get unseen Alert counts

```json
{
  "you": 3,
  "followedEvent": 0,
  "followedUser": 1
}
```
This route returns the number of alerts that are currently unseen for the user, broken down by category.

### HTTP Request

`GET https://node.ucic.vc/api/v04/alert/unseen`

## newFollower

```json
{
  "id": "75b94e65-b8ca-48a2-b7fd-d25e4d4b6772",
  "type": "newFollowers",
  "date": "2017-10-30T22:58:51.000Z",
  "seen": true,
  "data": {
    "followers": [{
      "userId": 414863,
      "userName": "Hi",
      "avatar": null,
      "badge": "https://media.ucic.vc/assets/tags/CA.png"
    },
    {
      "userId": 414869,
      "userName": "ab333",
      "avatar": null,
      "badge": "https://media.ucic.vc/assets/tags/CA.png"
    }]
  }
}
```
**Category: `you`**  
Generated when you get a new follower. Additional followers stack on the same alert while it is unseen.

##contentLikeReceive
```json
[{
  "id": "d25a0f9f-8b26-449a-b5ce-dfe302d6c1d1",
  "type": "contentLikeReceive",
  "date": "2017-10-31T17:36:55.000Z",
  "seen": true,
  "itemType": "response",
  "itemId": "E95E09CC-6901-46AB-A207-A399069EABA7",
  "data": {
    "eventTitle": "The Best Test Event ",
    "eventId": "1234567890",
    "likedItemType": "comment",
    "otherLikers": 4,
    "latestUser": {
      "userId": 414852,
      "userName": "Good",
      "avatar": null,
      "badge": "https://media.ucic.vc/assets/tags/CA.png"
    },
    "comment": {
      "text": "A comment for the ages"
    }
  }
},{
  "id": "fcb3471e-fdd5-4a36-b2b7-c44dd1b08dd5",
  "type": "contentLikeReceive",
  "date": "2017-10-31T17:10:25.000Z",
  "seen": true,
  "itemType": "question",
  "itemId": "301166",
  "data": {
    "eventTitle": "The Best Test Event ",
    "eventId": "1234567890",
    "likedItemType": "question",
    "otherLikers": 1,
    "latestUser": {
      "userId": 414816,
      "userName": "Trina Lee",
      "avatar": null,
      "badge": "https://media.ucic.vc/assets/tags/CA.png"
    },
    "question": {
      "text": "The 2nd Best Test Question"
    }
  }
},{
  "id": "234e621f-bb07-4a36-ba32-f0ce310021db",
  "type": "contentLikeReceive",
  "date": "2017-10-31T16:02:31.000Z",
  "seen": true,
  "itemType": "media",
  "itemId": "B_195685_1507756538",
  "data": {
    "eventTitle": "PCR TT - OCTOBER SWCP FUNDRAISER",
    "eventId": "evBrt_36682622712",
    "itemType": "media",
    "itemId": "B_195685_1507756538",
    "likedItemType": "media",
    "otherLikers": 4,
    "latestUser": {
      "userId": 414860,
      "userName": "Someone",
      "avatar": null,
      "badge": null
    },
    "media": {
      "id": "B_195685_1507756538",
      "MI": 76165,
      "mimeType": "video/mp4",
      "url": "https://media.ucic.vc/media/B_195685_1507756538/original.mp4",
      "thumb": "https://media.ucic.vc/media/10C52B61-97A9-492F-AFD9-4286E620BFD7/thumb.jpg"
    }
  }
}]
```
**Category: `you`**  

Generated when someone likes a piece of your content. Note that the alert always includes a `latestUser` object which denotes the most recent person to like a given piece of content. Multiple likes on the same content are collapsed into the same alert. The `data.otherLikers` is the running total of likes on the given content **minus** yourself and the `latestUser`, so this count may be used directly in a statement like "**Trina Lee** and **1** others liked your question" where **1** is the `otherLikers` count.   
Note, the `data.likedItemType` indicates what type of content was actually liked (not the `itemType` at the root level, which may be different when a comment is liked). This also corresponds to what additional data will be included as `data.{likedItemType}` (ex. `data.media` when `data.likedItemType` == `media`)

## responseReceive

```json
{
  "id": "bec6706b-5d48-48e3-9c88-74b95cab427c",
  "type": "responseReceive",
  "date": "2017-10-31T18:04:44.000Z",
  "seen": true,
  "itemType": "response",
  "itemId": "C23E68ED-BC85-448C-99F0-461050A11F16",
  "data": {
    "eventTitle": "The Best Test Event ",
    "eventId": "1234567890",
    "user": {
      "userId": 414867,
      "userName": "Someone",
      "avatar": null,
      "badge": "https://media.ucic.vc/assets/tags/CA.png"
    },
    "media": {
      "id": "C23E68ED-BC85-448C-99F0-461050A11F16",
      "MI": 76193,
      "mimeType": "image/jpeg",
      "url": "https://media.ucic.vc/media/C23E68ED-BC85-448C-99F0-461050A11F16/display.jpg",
      "thumb": "https://media.ucic.vc/media/C23E68ED-BC85-448C-99F0-461050A11F16/thumb.jpg"
    }
  }
}
```
**Category: `you`**  
Generated when someone responds to one of your requests.

## commentReceive

```json
{
  "id": "3787838b-290a-460e-8cec-28ff7cf69583",
  "type": "commentReceive",
  "date": "2017-11-01T13:39:55.000Z",
  "seen": true,
  "itemType": "media",
  "itemId": "140C0B18-2142-4D77-9A24-E853292A0E47",
  "data": {
    "eventTitle": "The Best Test Event ",
    "eventId": "1234567890",
    "latestUser": {
      "userId": 414865,
      "userName": "Trisha Sharma",
      "avatar": null,
      "badge": "https://media.ucic.vc/assets/tags/CA.png"
    },
    "commentCount": 1,
    "uniqueOtherCommentingUserCount": 0,
    "comment": {
      "text": "One of comments on media"
    }
  }
},{
  "id": "81b3f571-efeb-4870-a144-76347be2a1e3",
  "type": "commentReceive",
  "date": "2017-11-01T13:36:17.000Z",
  "seen": true,
  "itemType": "response",
  "itemId": "8A7EE382-33CC-4797-BDBC-79E13CFCF3EC",
  "data": {
    "eventTitle": "The Best Test Event ",
    "eventId": "1234567890",
    "itemType": "response",
    "itemId": "8A7EE382-33CC-4797-BDBC-79E13CFCF3EC",
    "latestUser": {
      "userId": 414865,
      "userName": "Trisha Sharma",
      "avatar": null,
      "badge": "https://media.ucic.vc/assets/tags/CA.png"
    },
    "commentCount": 2,
    "uniqueOtherCommentingUserCount": 1
  }
}

```
**Category: `you`**  
Generated when someone adds a comment to one of your media items. Comments on the same piece of media stack onto the same alert. Note that the data only includes the text of the comment when there is only 1 comment from 1 user. This is based on the UI designs for this alert, where it only makes sense to include the actual text of the comment while the alert is only referring to a single comment, rather than multiple.

## followOnComment

```json
{
  "id": "9f1898e5-c872-4372-a401-28e3455c76d6",
  "type": "followOnComment",
  "date": "2017-11-01T13:58:14.000Z",
  "seen": true,
  "itemType": "response",
  "itemId": "C23E68ED-BC85-448C-99F0-461050A11F16",
  "data": {
    "eventTitle": "The Best Test Event ",
    "eventId": "1234567890",
    "commentId": "df67fbed-853d-460d-95d5-10e7779ba624",
    "user": {
      "userId": 414863,
      "userName": "Hi",
      "avatar": null,
      "badge": "https://media.ucic.vc/assets/tags/CA.png"
    },
    "comment": {
      "text": "Non-Khan Khomment 5"
    }
  }
}
```
**Category: `you`**  
Generated when someone comments on an item after you comment on it. Only generated for the first comment after one of yours. Note that comments on the same item from the same user will replace the existing alert for this combination if you comment again and then the same user comments again.

## eventMedia

```json
{
  "id": "c611e16d-b99d-4707-a42e-863257e362a5",
  "type": "eventMedia",
  "date": "2017-11-01T14:52:22.000Z",
  "seen": true,
  "itemType": "media",
  "itemId": "714033A2-C854-420E-8C60-C3D0599A9123",
  "data": {
    "eventTitle": "The Best Test Event ",
    "eventId": "1234567890",
    "mimeType": "image/jpeg",
    "user": {
      "userId": 414863,
      "userName": "Hi",
      "avatar": null,
      "badge": "https://media.ucic.vc/assets/tags/CA.png"
    },
    "media": {
      "id": "714033A2-C854-420E-8C60-C3D0599A9123",
      "MI": 76195,
      "mimeType": "image/jpeg",
      "url": "https://media.ucic.vc/media/714033A2-C854-420E-8C60-C3D0599A9123/display.jpg",
      "thumb": "https://media.ucic.vc/media/714033A2-C854-420E-8C60-C3D0599A9123/thumb.jpg"
    }
  }
}
```
**Category: `followedEvent`**  
Generated when someone adds a piece of media to an event that you follow.

## eventComments

```json
[{
  "id": "7f2d841a-b30a-419b-96b6-814236faf081",
  "type": "eventComments",
  "date": "2017-11-01T14:34:15.000Z",
  "seen": true,
  "itemType": "comment",
  "itemId": "bc93be56-74f3-488b-9b99-0382a0dbc590",
  "data": {
    "eventTitle": "The Best Test Event ",
    "eventId": "1234567890",
    "itemType": "comment",
    "itemId": "0d8513f6-dddb-4852-810c-4ad0bb3874e0",
    "since": "2017-11-01T14:34:06.000Z",
    "latestUser": {
      "userId": 414865,
      "userName": "Trisha Sharma",
      "avatar": null,
      "badge": "https://media.ucic.vc/assets/tags/CA.png"
    },
    "commentCount": 2,
    "uniqueCommentingUserCount": 2
  }
},{
  "id": "fbf964c4-6fb5-4bbf-be9b-59c1ae0e3149",
  "type": "eventComments",
  "date": "2017-11-01T14:27:41.000Z",
  "seen": true,
  "itemType": "comment",
  "itemId": "5856c686-14b5-46d8-b028-421941501ec4",
  "data": {
    "eventTitle": "The Best Test Event ",
    "eventId": "1234567890",
    "since": "2017-11-01T14:27:39.000Z",
    "latestUser": {
      "userId": 414865,
      "userName": "Trisha Sharma",
      "avatar": null,
      "badge": "https://media.ucic.vc/assets/tags/CA.png"
    },
    "commentCount": 1,
    "uniqueCommentingUserCount": 1,
    "comment": {
      "text": "Comment on followed event 3"
    }
  }
}]
```
**Category: `followedEvent`**  
Generated when someone adds a comment to an event you follow. Note that multiple comments added to the same event will stack on the same alert while the alert is unseen. Note also that the comment text is only included when the alert refers to a single comment.

## eventQuestions

```json
[{
  "id": "8c94329f-533a-42ab-8223-e1c960d03c70",
  "type": "eventQuestions",
  "date": "2017-11-01T19:22:18.000Z",
  "seen": true,
  "itemType": null,
  "itemId": null,
  "data": {
    "eventId": "1234567890",
    "eventTitle": "The Best Test Event ",
    "since": "2017-11-01T19:11:51.000Z",
    "latestUser": {
      "userId": 414865,
      "userName": "Trisha Sharma",
      "avatar": null,
      "badge": "https://media.ucic.vc/assets/tags/CA.png"
    },
    "questionCount": 3,
    "uniqueAskingUserCount": 2
  }
},{
  "id": "d540b584-7029-4278-8f7d-29e221104bfd",
  "type": "eventQuestions",
  "date": "2017-11-01T18:59:14.000Z",
  "seen": true,
  "itemType": null,
  "itemId": null,
  "data": {
    "eventId": "1234567890",
    "eventTitle": "The Best Test Event ",
    "since": "2017-11-01T18:55:19.814Z",
    "latestUser": {
      "userId": 414865,
      "userName": "Trisha Sharma",
      "avatar": null,
      "badge": "https://media.ucic.vc/assets/tags/CA.png"
    },
    "questionCount": 1,
    "uniqueAskingUserCount": 1,
    "question": {
      "text": "The 13th Best Test Question"
    }
  }
}]
```
**Category: `followedEvent`**  
Generated when someone adds a question to an event you follow. Note that multiple questions added to the same event will stack on the same alert while the alert is unseen. Note also that the question text is only included when the alert refers to a single question.

## followUserMedia

```json
{
  "id": "72098985-4232-4f45-93c6-6fcb2ceb27fe",
  "type": "followUserMedia",
  "date": "2017-11-01T20:03:48.000Z",
  "seen": true,
  "itemType": null,
  "itemId": null,
  "data": {
    "user": {
      "userId": 227108,
      "userName": "Sir_issac",
      "avatar": null,
      "badge": "https://media.ucic.vc/assets/tags/DZ.png"
    },
    "medias": [{
      "id": "23A225CF-FB12-4121-8DC1-715873EF4B8A",
      "MI": 76199,
      "mimeType": "image/jpeg",
      "url": "https://media.ucic.vc/media/23A225CF-FB12-4121-8DC1-715873EF4B8A/display.jpg",
      "thumb": "https://media.ucic.vc/media/23A225CF-FB12-4121-8DC1-715873EF4B8A/thumb.jpg"
    },{
      "id": "348AC3DC-A57B-4C31-A937-30C1615CF69C",
      "MI": 76200,
      "mimeType": "image/jpeg",
      "url": "https://media.ucic.vc/media/348AC3DC-A57B-4C31-A937-30C1615CF69C/display.jpg",
      "thumb": "https://media.ucic.vc/media/348AC3DC-A57B-4C31-A937-30C1615CF69C/thumb.jpg"
    }]
  }
}
```
**Category: `followedUser`**  
Generated when someone you follow adds media. Note that media for the same user stack while the alert is unread. The idea is for the client to open the followed user's "sent" media profile section with the alert.

## followedUserComment

```json
{
   "id": "12f13b21-ecc4-4514-af66-5d0a2bca5cf6",
   "type": "followedUserComment",
   "date": "2017-11-01T20:14:46.000Z",
   "seen": true,
   "itemType": "comment",
   "itemId": "6fbbddb8-2b44-447a-994e-c7b429c9f935",
   "data": {
     "eventId": "P7jsRKmjzod6AErynK",
     "eventTitle": "Curren$y",
     "commentId": "6fbbddb8-2b44-447a-994e-c7b429c9f935",
     "user": {
       "userId": 227108,
       "userName": "Sir_issac",
       "avatar": null,
       "badge": "https://media.ucic.vc/assets/tags/DZ.png"
     },
     "comment": {
       "text": "Commmmment 2"
     }
   }
}
```
**Category: `followedUser`**  
Generated when someone you follow comments on something. 

## followedUserLikedQuestion

```json
{
   "id": "1ea412d0-fa56-4a57-9dda-bab55d25b5ff",
   "type": "followedUserLikedQuestion",
   "date": "2017-11-01T20:27:01.000Z",
   "seen": true,
   "itemType": "question",
   "itemId": "301255",
   "data": {
     "eventTitle": "The Best Test Event ",
     "eventId": "1234567890",
     "user": {
       "userId": 227108,
       "userName": "Sir_issac",
       "avatar": null,
       "badge": "https://media.ucic.vc/assets/tags/DZ.png"
     },
     "question": {
       "text": "The 15th Best Test Question"
     }
   }
}
```
**Category: `followedUser`**  
Generated when someone you follow likes a question.

## followedUserLikedComment

```json
{
  "id": "c8732b97-4741-4101-b6f4-9e261556a0d3",
  "type": "followedUserLikedComment",
  "date": "2017-11-02T14:15:23.000Z",
  "seen": true,
  "itemType": "response",
  "itemId": "C23E68ED-BC85-448C-99F0-461050A11F16",
  "data": {
    "eventTitle": "The Best Test Event ",
    "eventId": "1234567890",
    "commentId": "460e7bee-54fb-41f0-9825-34eaf546200f",
    "user": {
      "userId": 227108,
      "userName": "Sir_issac",
      "avatar": null,
      "badge": "https://media.ucic.vc/assets/tags/DZ.png"
    },
    "comment": {
      "text": "One of comments."
    }
  }
}
```
**Category: `followedUser`**  
Generated when someone you follow likes a comment.

## followedUserLikedMedia

```json
{
  "id": "adbffe6e-1080-4af3-995a-a971a3d72ab3",
  "type": "followedUserLikedMedia",
  "date": "2017-11-02T14:47:51.000Z",
  "seen": true,
  "data": {
    "eventTitle": "The Best Test Event ",
    "eventId": "1234567890",
    "user": {
      "userId": 227108,
      "userName": "Sir_issac",
      "avatar": null,
      "badge": "https://media.ucic.vc/assets/tags/DZ.png"
    },
    "medias": [{
      "id": "E95E09CC-6901-46AB-A207-A399069EABA7",
      "MI": 76113,
      "url": "https://media.ucic.vc/media/E95E09CC-6901-46AB-A207-A399069EABA7/display.jpg",
      "thumb": "https://media.ucic.vc/media/E95E09CC-6901-46AB-A207-A399069EABA7/thumb.jpg",
      "mimeType": "image/jpeg"
    }]
  }
}
```
**Category: `followedUser`**  
Generated when someone you follow likes a piece of media. Note that the same user liking multiple media will stack on the same alert while it is unseen. The idea is for the client to link to the followed user's "liked" media profile section from the alert.

## followedUserFollowed

```json
{
  "id": "68074f85-a77b-4f83-b8f9-e015bc52a924",
  "type": "followedUserFollowed",
  "date": "2017-11-02T14:57:00.000Z",
  "seen": true,
  "itemType": null,
  "itemId": null,
  "data": {
    "user": {
      "userId": 227108,
      "userName": "Sir_issac",
      "avatar": null,
      "badge": "https://media.ucic.vc/assets/tags/DZ.png"
    },
    "newFollowees": [{
      "userId": 414853,
      "userName": "H",
      "avatar": null,
      "badge": "https://media.ucic.vc/assets/tags/CA.png"
    }, {
      "userId": 414854,
      "userName": "PixelApi25Berlin",
      "avatar": null,
      "badge": "https://media.ucic.vc/assets/tags/DE.png"
    }]
  }
}
```
**Category: `followedUser`**  
Generated when someone you follow follows someone. Note that the same followee following multiple users will stack on the same alert while it is unseen. Client should link to the followee's "followed users" profile section from the alert.