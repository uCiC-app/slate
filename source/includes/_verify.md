# Verify

## Verify Content

```shell
curl -X POST -H "Authorization: <AUTHORIZATION_TOKEN>" -H "Content-Type: application/json" -d '{ "itemType": "event", "itemId": "1234567890", "verify": true }' "https://node.ucic.vc/api/v04/verify"
```
```javascript

```

> The above command returns a 204 status code upon success

```json

```

This endpoint lets the client confirm or deny that a piece of content is valid. Currently, only `event` itemType is supported, but more may be added in the future. The body param `verify` is supplied as a boolean to indicate that the event is (true), or isn't (false) happening.   

Events with a verification score lower than 3 will have an "[Unconfirmed]" tag at the front of the title. Events with a vScore lower than zero will no longer be returned by the map/list view.

### HTTP Request

`POST https://node.ucic.vc/api/v04/report/content`

### Request Body

| Parameter | Type    | Description                              |
| --------- | ------- | ---------------------------------------- |
| itemType  | String  | currently just 'event'                   |
| itemId    | String  | The identifier of the entity being verified. |
| verify    | Boolean | `true` if the client user is verifying the event, `false` if they are debunking it. |

### Errors

| Code | Error                                    | Description                              |
| ---- | ---------------------------------------- | ---------------------------------------- |
| 400  | missing or invalid itemType in request body | Client sent an invalid or missing value for `itemType` |
| 400  | missing itemId and/or verify req body params | Client did not include an `itemId` and/or `verify` in the request |

