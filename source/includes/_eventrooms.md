# Event Rooms 

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
    "icon": "https://s3-us-west-2.amazonaws.com/ucic-production/assets/events/news.png",
    "name": "The Best Test Event",
    "description": "A Dummy event created to centralize testing of various event room aspects",
    "categoryId": "news",
    "category": "News",
    "rank": 85,
    "participantCount": 99,
    "mediaCount": 99,
    "location": {
      "lat": 47.13412,
      "lon": 33.124105
    },
    "radius": 1000,
    "start": "2017-08-02T00:05:00.000Z",
    "end": "2017-08-31T00:05:00.000Z",
    "active": true
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
            "avatar": null,
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
        "type": "comment",
        "date": "2017-08-02T20:59:01.000Z",
        "id": "03ba5137-0ca6-4073-bdcd-8a92dcb772fe",
        "eventId": "1234567890",
        "popularCount": 2,
        "atEvent": false,
        "creator": {
            "userId": 414767,
            "userName": "Someone",
            "avatar": null,
            "badge": null
        },
        "comment": {
            "text": "This is a root level comment!",
            "comments": [
                {
                    "creator": {
                        "userId": 414767,
                        "userName": "Someone",
                        "avatar": null,
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

**Note:** When following a question, use the question version of the follow/unfollow routes and provide the value of `item.question.followId` as the idenfier in the url

### HTTP Request

`PUT https://node.ucic.vc/api/v04/events/<ID>`

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



