# Comments 

## Get a Card's Comments

```shell
curl "https://node.ucic.vc/api/v05/card/DEC604AC-C29F-4764-B9C6-2CEC7351ABB6/comments"  -H "Authorization: <AUTHORIZATION_TOKEN>"
```
```javascript

```

> The above command returns JSON structured like this:

```json
[
  {
    "id": "7CFFE67B-D74A-4EBC-9D0B-04AA18F540B1",
    "text": "Adding a comment to a card",
    "itemId": "DEC604AC-C29F-4764-B9C6-2CEC7351ABB6",
    "itemType": "card",
    "createdAt": "2016-12-18T22:18:04.000Z",
    "creator": {
      "UI": "611",
      "badge": "https://media.ucic.vc/assets/tags/RU.png",
      "avatar": "http://staging-media.ucic.vc/media/8D33E7DA-D1FC-4DA4-B787-987916062D6D/thumb.png",
      "Username": "John Doe"
    }
  }
]
```

This endpoint retrieves the comments for a card.  Comments are sorted in descending createdAt order.

### HTTP Request

`GET https://node.ucic.vc/api/v05/cards/<ID>/comments`

### URL Parameters

| Parameter | Type | Description                              |
| --------- | ---- | ---------------------------------------- |
| ID        | UUID | The ID of the card to retrieve comments for |

### Query Parameters

| Parameter | Type             | Description                              |
| --------- | ---------------- | ---------------------------------------- |
| limit     | Unsigned Integer | Maximum number of comments to return     |
| offset    | Unsigned Integer | Offset in list of commentss to start return from |
| page      | Unsigned Integer | Page of comments to return               |
| sort      | String           | what to sort returned comments by, currently only supports `createdAt` |
| order     | String           | Either `ASC` or `DESC`                   |


## Create a Comment for a Card

```shell
curl -X POST -H "Authorization: <AUTHORIZATION_TOKEN>" -H "Content-Type: application/json" -d '{ "text": "Adding a comment to a card" }' "https://node.ucic.vc/api/v05/card/DEC604AC-C29F-4764-B9C6-2CEC7351ABB6/comments"
```
```javascript

```

> The above command returns Created 201 with the new comment:

```json
{
  "comment": {
    "id": "f722ae64-afca-4fde-9599-51c132dd0ec8",
    "text": "old comment route on card verify same response",
    "itemId": "B5C0E281-7EC7-4A62-90C9-50BB872A5729",
    "itemType": "card",
    "createdAt": "2017-08-24T16:07:10.000Z",
    "creator": {
      "UI": "195685",
      "avatar": "https://media.ucic.vc/media/4A0F0DEA-16E9-49E0-B3C0-5AC38FD759E8/micro.jpg",
      "Username": "Khan",
      "badge": "https://media.ucic.vc/assets/tags/CA.png"
    }
  }
}
```

This endpoint creates a comment for a card.

### HTTP Request

`POST https://node.ucic.vc/api/v05/cards/<ID>/comments`

### URL Parameters

| Parameter | Type | Description                            |
| --------- | ---- | -------------------------------------- |
| ID        | UUID | The ID of the card to create a comment |

### Request Body

| Parameter | Type   | Description           |
| --------- | ------ | --------------------- |
| text      | String | The comment body text |

## Create a Comment on an Arbitrary Entity

```shell
curl -X POST -H "Authorization: <AUTHORIZATION_TOKEN>" -H "Content-Type: application/json" -d '{ "text": "Adding a comment to an event", "itemType": "event", "itemId": "1234567890" }' "https://node.ucic.vc/api/v04/comment/new"
```
```javascript

```

> The above command returns Created 201 with the new comment:

```json
{
  "comment": {
    "id": "b70c9f59-b4ab-4e10-adfe-50abd7b136bc",
    "text": "one more on the new route with updated return values",
    "itemId": "B5C0E281-7EC7-4A62-90C9-50BB872A5729",
    "itemType": "card",
    "createdAt": "2017-08-24T16:07:03.000Z",
    "creator": {
      "UI": "195502",
      "avatar": "https://media.ucic.vc/media/7C21E547-277A-4A23-934A-E7986B82E5EB/micro.jpg",
      "Username": "Jan",
      "badge": "https://media.ucic.vc/assets/tags/CA.png"
    }
  }
}
```

This endpoint creates a comment for:

- a card/media item  
- an event room  
- as a reply to an existing comment  
- an external media  

When using it, the POST body specifies the target item being commented on with the `itemType` field (supports `event`, `comment`, `extMedia`, `card`) and the identifier of the target item with the `itemId` field.   

See the [Supported Entites table](https://ucic-app.github.io/ucic-docs/#get-comments-for-an-arbitrary-entity) below for more details about which id to use with each itemType.  

**Note:** the itemTypes `card` and `media` are interchangeable. Also note that when using `media`, the returned json for the created comment will have an itemType of `card`.

### HTTP Request

`POST https://node.ucic.vc/api/v04/comment/new`

### Request Body  
All 3 body params are required.

| Parameter | Type   | Description                              |
| --------- | ------ | ---------------------------------------- |
| text      | String | The comment body text                    |
| itemType  | String | The type of item being commented on. Currently either `event`, `comment`, or `extMedia`, `card`, `media` |
| itemId    | String | The unique identifier of the object being commented on. This is the `comment.id` in the case of a comment on a comment and `event.id` in the event of an event room. |

### Errors
| Code | Text                        | Description                              |
| ---- | --------------------------- | ---------------------------------------- |
| 400  | Missing body item/type/text | One or more required body params are missing |
| 201  | *see Silent Failure below*  | *see Silent Failure below*               |

###Silent Failure
If profanity is detected in the comment, the server fails pseudo-silently to create the comment. The code returned is still a 201 success, however, the json reply will look like this: 

```
{
  "comment": {
    "id": "ProfanityDetected.CommentNotCreated",
    "text": "shit",
    "itemId": "B5C0E281-7EC7-4A62-90C9-50BB872A5729",
    "itemType": "card",
    "hidden": true
  }
}
```

## Get Comments for an Arbitrary Entity

```shell
curl -H "Authorization: <AUTHORIZATION_TOKEN>" "https://node.ucic.vc/api/v04/comments"
```
```javascript

```

>The above command returns an array of comments for the specified entity

```json
[{
  "id": "258c5ef4-3409-431c-81d6-fc4e891ec5a7",
  "text": "one more on the new route with string creator ui",
  "itemId": "B5C0E281-7EC7-4A62-90C9-50BB872A5729",
  "itemType": "card",
  "createdAt": "2017-08-24T15:10:58.000Z",
  "creator": {
    "UI": "195685",
    "avatar": "https://media.ucic.vc/media/4A0F0DEA-16E9-49E0-B3C0-5AC38FD759E8/micro.jpg",
    "Username": "Khan",
    "badge": "https://media.ucic.vc/assets/tags/CA.png"
  }
}]
```

This endpoint retrieves a list of comment for various entities listed below. When fetching comments from the route, the client must specify an itemType and itemId in the query parameters (along with the optional, standard pagination params).

### Supported Entities
| Entity                              | itemType          | itemId                                   |
| ----------------------------------- | ----------------- | ---------------------------------------- |
| Card/Media                          | `card` or `media` | The non-MI id of the card or media. Ie. `card.id` or `cardId`. Note: the `itemType` on the returned comments will always read `card` |
| External Media                      | `extMedia`        | `extMediaRoomItem.id`                    |
| Comment (fetch subcomments/replies) | `comment`         | `comment.id`                             |
| Event Room                          | `event`           | `event.id`                               |


### HTTP Request

`GET https://node.ucic.vc/api/v04/comment`

### Query Parameters

| Parameter        | Type    | Description                              |
| ---------------- | ------- | ---------------------------------------- |
| itemType (req'd) | String  | See Supported Entities table above       |
| itemId (req'd)   | String  | See Supported Entities table above       |
| limit            | Integer | Maximum number of comments to return     |
| offset           | Integer | Where in the list of comments to start the return from |
| sort             | String  | what to sort returned comments by, currently only supports createdAt |
| order            | String  | Either ASC or DESC                       |

### Errors
| Code | Text                  | Description                              |
| ---- | --------------------- | ---------------------------------------- |
| 400  | No itemId or itemType | One or more required query params are missing |