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

This endpoint lets the client register a "like" on a specified entity. Currently supports 2 entities as targets for the like: 

- `media` (use the `MI` as the `itemId`)
- `extMedia` (use the `eventRoomItem.id` as the `itemId`)

### HTTP Request

`POST https://node.ucic.vc/api/v04/like`

### Request Body

| Parameter | Type   | Description                              |
| --------- | ------ | ---------------------------------------- |
| itemType  | String | `media` or `extMedia`                    |
| itemId    | String | The identifier of the entity being liked. Use the `MI` for `media` itemType and `eventRoomItem.id` for `extMedia` itemType |

### Errors

| Code | Error                  | Description                              |
| ---- | ---------------------- | ---------------------------------------- |
| 400  | Invalid itemType param | Client sent an invalid value for itemType |
| 400  | Missing itemId         | Client did not include an itemId in the request |