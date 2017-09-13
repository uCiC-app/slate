# Report

## Report Content

```shell
curl -X POST -H "Authorization: <AUTHORIZATION_TOKEN>" -H "Content-Type: application/json" -d '{ "itemType": "media", "itemId": "76092" }' "https://node.ucic.vc/api/v04/report/content"
```
```javascript

```

> The above command returns a 204 status code upon success

```json

```

This endpoint lets the client report a piece of content. The content will no longer be served to the reporting client. The system will also eventually remove content that has been reported multiple times from tbeing served to *any* clients. The route currently supports reporting the following item types: 

- `media` (use the numeric `MI` as the `itemId`)
- `extMedia` (use the `eventRoomItem.id` as the `itemId`)
- `comment` (use the `comment.id` as the `itemId`)
- `question` (use the numeric `requestId` as the `itemId` )

### HTTP Request

`POST https://node.ucic.vc/api/v04/report/content`

### Request Body

| Parameter | Type   | Description                              |
| --------- | ------ | ---------------------------------------- |
| itemType  | String | `media`, `extMedia`, `comment`, or `question` |
| itemId    | String | The identifier of the entity being reported. See info above for information on which id to use for each type of entity. |

### Errors

| Code | Error                  | Description                              |
| ---- | ---------------------- | ---------------------------------------- |
| 400  | Invalid itemType param | Client sent an invalid value for itemType |
| 400  | Missing itemId         | Client did not include an itemId in the request |

