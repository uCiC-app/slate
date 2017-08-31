# Like

## Like an Entity

```shell
curl -X POST -H "Authorization: <AUTHORIZATION_TOKEN>" -H "Content-Type: application/json" -d '{ "itemType": "media", "itemId": "76092" }' "https://node.ucic.vc/api/v04/like"

```
```javascript

```

> The above command returns a 204 status code upon success

```json

```

This endpoint lets the client register a "like" on a specified entity. Currently supports 4 entities as targets for the like: 

- `media` (use the `MI` as the `itemId`)
- `extMedia` (use the `eventRoomItem.id` as the `itemId`)
- `comment` (use the `comment.id` as the `itemId`)
- `question` (use the numeric `requestId` as the `itemId` )

### HTTP Request

`POST https://node.ucic.vc/api/v04/like`

### Request Body

| Parameter | Type   | Description                              |
| --------- | ------ | ---------------------------------------- |
| itemType  | String | `media`, `extMedia`, `comment`, or `question` |
| itemId    | String | The identifier of the entity being liked. See info above for information on which id to use for each type of entity. |

### Errors

| Code | Error                  | Description                              |
| ---- | ---------------------- | ---------------------------------------- |
| 400  | Invalid itemType param | Client sent an invalid value for itemType |
| 400  | Missing itemId         | Client did not include an itemId in the request |


## Unlike an Entity

```shell
curl -X POST -H "Authorization: <AUTHORIZATION_TOKEN>" -H "Content-Type: application/json" -d '{ "itemType": "media", "itemId": "76092" }' "https://node.ucic.vc/api/v04/like/revoke"

```
```javascript

```

> The above command returns a 204 status code upon success

```json

```

This endpoint lets the client remove their "like" on a specified, previously liked entity. Currently supports 4 entities as targets for the unlike: 

- `media` (use the `MI` as the `itemId`)
- `extMedia` (use the `eventRoomItem.id` as the `itemId`)
- `comment` (use the `comment.id` as the `itemId`)
- `question` (use the numeric `requestId` as the `itemId` )

### HTTP Request

`POST https://node.ucic.vc/api/v04/like/revoke`

### Request Body

| Parameter | Type   | Description                              |
| --------- | ------ | ---------------------------------------- |
| itemType  | String | `media`, `extMedia`, `comment`, or `question` |
| itemId    | String | The identifier of the entity being liked. See info above for information on which id to use for each type of entity. |

### Errors

| Code | Error                  | Description                              |
| ---- | ---------------------- | ---------------------------------------- |
| 400  | Invalid itemType param | Client sent an invalid value for itemType |
| 400  | Missing itemId         | Client did not include an itemId in the request |