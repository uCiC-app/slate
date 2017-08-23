# Event Rooms 

## Get list of event rooms

```shell

curl "https://node.ucic.vc/api/v04/eventRoom/list" -H "Authorization: <AUTHORIZATION_TOKEN>"
```

```javascript

```
> The above command returns JSON structured like this:

```json
[{
  "id": "1234567890",
  "title": "The Best Test Event",
  "description": "A Dummy event created to centralize testing of various event room aspects",
  "categoryId": "news",
  "scope": "locality",
  "country": "UN",
  "city": null,
  "region": null,
  "location": {
    "lat": 47.3302,
    "lon": -29.5989
  },
  "radius": 1000,
  "mediaCount": 13,
  "rank": 85,
  "start": "2017-08-09T08:05:00.000Z",
  "end": "2017-08-31T00:05:00.000Z",
  "active": true,
  "lastMediaLike": "2017-08-15T15:15:53.000Z",
  "lastMediaPost": "2017-08-15T15:15:53.000Z",
  "categoryName": "News",
  "categoryIcon": "https://s3-us-west-2.amazonaws.com/ucic-production/assets/events/news.png",
  "followerCount": 2,
  "youFollowEvent": true,
  "latestMedia": {
    "video": false,
    "thumb": "https://media.ucic.vc/media/fba18fda-1986-4abb-8e96-fb24f70ad9bd/thumb.jpg"
  },
  "participantCount": 99
}]
```

This route returns a list of event rooms that contain a minimum of one piece of media.

### HTTP Request

`GET https://node.ucic.vc/api/v04/eventRoom/list`

### Query Parameters

| Parameter  | Type    | Description                              |
| ---------- | ------- | ---------------------------------------- |
| sort       | String  | The type of sort to apply. Currently supports `live`, `popular`, `following` |
| categories | String  | A comma-seperated list of event category IDs to return. Use the GET /map/eventCategories route below to retrive the list of supported event categories. Example usage in query url: &categories=sports,culture,shows. If omitted, event rooms of any category may be returned |
| limit      | integer | The maximum number of event rooms to return |
| offset     | integer | The number of event rooms to skip in the return for paginating results |

## Get Event Room info

```shell

curl "https://node.ucic.vc/api/v04/eventRoom/:id" -H "Authorization: <AUTHORIZATION_TOKEN>"
```

```javascript

```

> The above command returns JSON structured like this:

```json
{
  "id": "1234567890",
  "title": "The Best Test Event",
  "description": "A Dummy event created to centralize testing of various event room aspects",
  "categoryId": "news",
  "scope": "locality",
  "country": "UN",
  "city": null,
  "region": null,
  "location": {
    "lat": 47.3302,
    "lon": -29.5989
  },
  "radius": 1000,
  "mediaCount": 13,
  "rank": 85,
  "start": "2017-08-09T08:05:00.000Z",
  "end": "2017-08-31T00:05:00.000Z",
  "lastMediaLike": "2017-08-15T15:15:53.000Z",
  "lastMediaPost": "2017-08-15T15:15:53.000Z",
  "active": true,
  "categoryName": "News",
  "categoryIcon": "https://s3-us-west-2.amazonaws.com/ucic-production/assets/events/news.png",
  "followerCount": 2,
  "youFollowEvent": true,
  "latestMedia": {
    "video": false,
    "thumb": "https://media.ucic.vc/media/fba18fda-1986-4abb-8e96-fb24f70ad9bd/thumb.jpg"
  },
  "participantCount": 99
}
```

This endpoint retrieves the high level info for a given event room.

**Note:** radius is expressed in meters. 

### HTTP Request

`GET https://node.ucic.vc/api/v04/eventRoom/:id`

### URL Parameters

| Parameter | Type   | Description                              |
| --------- | ------ | ---------------------------------------- |
| id        | String | The id of the event room to retrieve the info for |

## Get Event Room Items

```shell
curl "https://node.ucic.vc/api/v04/eventRoom/:id/items" -H "Authorization: <AUTHORIZATION_TOKEN>"
```

```javascript

```

> The above command returns JSON structured like this:

```json
[
    {
        "type": "media",
        "date": "2017-08-03T16:44:40.000Z",
        "id": "A20E9361-78BD-4244-B867-22BC46537FA2",
        "eventId": "1234567890",
        "popularCount": 1,
        "atEvent": false,
        "creator": {
            "userId": 414744,
            "userName": "Alc",
            "userAvatar": null,
            "badge": "https://media.ucic.vc/assets/tags/CA.png"
        },
        "media": {
            "text": "Free floating media!",
            "cardId": "A20E9361-78BD-4244-B867-22BC46537FA2",
            "MI": 76055,
            "thumb": "https://media.ucic.vc/media/A20E9361-78BD-4244-B867-22BC46537FA2/thumb.jpg",
            "url": "https://media.ucic.vc/media/A20E9361-78BD-4244-B867-22BC46537FA2/original.png",
            "mimeType": "image/png",
            "likeCount": 1,
            "commentCount": 0,
            "liked": false
        }
    },
    {
        "type": "extMedia",
        "date": "2017-08-23T17:52:37.000Z",
        "id": "tweet_900415492589928448",
        "eventId": "e252c2bf-e58e-45ac-869c-43e0480dc77e",
        "popularCount": 1,
        "atEvent": true,
        "creator": {
            "userName": "Boat Sales",
            "userAvatar": "https://pbs.twimg.com/profile_images/656976062447026176/9vF-MU6-_normal.jpg",
            "badge": "https://media.ucic.vc/assets/tags/twitter/tweet.png"
        },
        "extMedia": {
            "source": "twitter/tweet",
            "attributionUrl": "https://t.co/3mTuWOP53U",
            "imageUrl": "https://pbs.twimg.com/media/DH7rHdzUAAATJ-S.jpg",
            "videoUrl": null,
            "extCreator": {
                "userHandle": "BoatSales",
                "userId": "4307191455"
            },
            "text": "On Twitter https://t.co/3mTuWOP53U",
            "likeCount": 0,
            "likers": [],
            "commentCount": 1,
            "commenters": [
                227131
            ]
        }
    },
    {
        "type": "comment",
        "date": "2017-08-02T20:59:01.000Z",
        "id": "03ba5137-0ca6-4073-bdcd-8a92dcb772fe",
        "eventId": "1234567890",
        "popularCount": 2,
        "atEvent": false,
        "creator": {
            "userId": 414767,
            "userName": "Someone",
            "userAvatar": null,
            "badge": null
        },
        "comment": {
            "text": "This is a root level comment!",
            "comments": [
                {
                    "creator": {
                        "userId": 414767,
                        "userName": "Someone",
                        "userAvatar": null,
                        "badge": null
                    },
                    "date": "2017-08-02T20:59:53.000Z",
                    "text": "This is an inner comment, replying to a root comment",
                    "atEvent": false
                }
            ]
        }
    },
    {
        "type": "question",
        "date": "2017-08-02T16:36:53.000Z",
        "id": "300651",
        "eventId": "1234567890",
        "popularCount": 1,
        "atEvent": false,
        "creator": {
            "userId": 414767,
            "userName": "Someone",
            "badge": null,
            "userAvatar": null
        },
        "question": {
            "text": "What's happening at this event?",
            "followId": "03dabda4-e8a0-4cdc-86ab-5235491beb1c",
            "followers": [
                {
                    "userId": 414767,
                    "userName": "Someone",
                    "userAvatar": null
                }
            ],
            "replies": [
                {
                    "creator": {
                        "userId": 414744,
                        "userName": "Alc",
                        "badge": "https://media.ucic.vc/assets/tags/CA.png",
                        "userAvatar": null
                    },
                    "date": "2017-08-03T18:33:39.000Z",
                    "text": "A reply to an event question",
                    "atEvent": false,
                    "cardId": "399E2745-28E0-4041-9A79-BEA80D5B0AD0",
                    "MI": 76056,
                    "thumb": "https://media.ucic.vc/media/399E2745-28E0-4041-9A79-BEA80D5B0AD0/thumb.jpg",
                    "url": "https://media.ucic.vc/media/399E2745-28E0-4041-9A79-BEA80D5B0AD0/original.jpeg",
                    "mimeType": "image/jpeg",
                    "likeCount": 1,
                    "commentCount": 0,
                    "liked": false
                }
            ]
        }
    }
]
```

This endpoint retrieves the list of items for the specified event room id.

### External Media

The admin dashboard allows us to import media from twitter for event rooms. Since it is largely external, there are some special considerations:

- `item.creator` does not have a `userId` property. Details to be finalized when happens when their avatar is clicked
- The item may have either an `imageUrl` or both an `imageUrl` and a `videoUrl`. If a `videoUrl` is present, the `imageUrl` is a preview thumbnail



**Note:** When following a question, use the question version of the follow/unfollow routes and provide the value of `item.question.followId` as the idenfier in the url

### HTTP Request

`GET https://node.ucic.vc/api/v04/eventRoom/<ID>/items`

### URL Parameters

| Parameter | Type   | Description                              |
| --------- | ------ | ---------------------------------------- |
| id        | String | The id of the event room to retrieve the items for |

### Query Parameters

| Parameter | Type                   | Description                              |
| --------- | ---------------------- | ---------------------------------------- |
| sort      | String                 | Sorted by most recent first. sort supports a value of 'popular' to bring interesting content to the front. |
| atEvent   | String                 | If a value of `true` is sent for this query param, only items that were generated at the location of the event will be sent (based on the root level item, atEvent of nested items is ignored) |
| filter    | Comma delimited String | A comma separated list of what item types to return. supports any combination of `question`, `media`, `comment` |



## Follow Event Room

```shell

curl "https://node.ucic.vc/api/v04/eventRoom/follow/:id" -H "Authorization: <AUTHORIZATION_TOKEN>"
```

```javascript

```

> The above command returns a 204 success response code  

This endpoint let's a user start following a given event room.

### HTTP Request

`GET https://node.ucic.vc/api/v04/eventRoom/follow/:id`

### URL Parameters

| Parameter | Type   | Description                        |
| --------- | ------ | ---------------------------------- |
| id        | String | The id of the event room to follow |

## Unfollow Event Room

```shell

curl "https://node.ucic.vc/api/v04/eventRoom/unfollow/:id" -H "Authorization: <AUTHORIZATION_TOKEN>"
```

```javascript

```

> The above command returns a 204 success response code  

This endpoint let's a user stop following a given event room.

### HTTP Request

`GET https://node.ucic.vc/api/v04/eventRoom/unfollow/:id`

### URL Parameters

| Parameter | Type   | Description                              |
| --------- | ------ | ---------------------------------------- |
| id        | String | The id of the event room to stop following |