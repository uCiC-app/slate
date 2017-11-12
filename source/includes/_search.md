# Search

## Search for Events and/or Users

```shell
curl -H "Authorization: <AUTHORIZATION_TOKEN>" "https://node.ucic.vc/api/v04/search/Something"

```
```javascript

```

> The above command returns the following json upon success

```json
{
  "users": [{
    "userId": "210243",
    "userName": "Dave",
    "userAvatar": "https://media.ucic.vc/media/https://media.ucic.vc/media/D4381BD9-5A61-4544-8B6B-EB0D329895CA/micro.jpg/thumb.jpg",
    "badge": "https://media.ucic.vc/assets/tags/US.png"
  }],
  "events": [{
    "id": "1234567890",
    "title": "The Best Test Event",
    "city": "Atlantis",
    "region": "Da Atlantic",
    "country": "UN",
    "categoryId": "news",
    "subCategoryIds": [
      "politicsNews"
    ]
  }]
}
```

This endpoint lets the client search for multiple types of entities at once with the same search string.    

**Note:** to avoid flooding the server with requests, it is recommended that the clients wait a handful of miliseconds between keystrokes of entered search text before sending the search request to the server.

### Placeholders
The endpoint is set up to return a few (up to 5) placeholder items of each supported type if it is hit with no search text in the param. Note that all query parameters are ignored if no search text is provided.

### HTTP Request

`GET https://node.ucic.vc/api/v04/search/:searchText`

### Url Paramaters

| Parameter  | Type   | Description                          |
| ---------- | ------ | ------------------------------------ |
| searchText | String | The user-entered text to search with |


### Query  Paramaters

| Parameter | Type                   | Description                              |
| --------- | ---------------------- | ---------------------------------------- |
| filter    | Comma delimited string | What types of entities to search for and return. Currently only supports `events` and `users`. If omitted, all supported types will be searched and returned |
| limit     | Integer                | maximum number of items to return **of each type** |
| offset    | Integer                | How many items to skip in the results if paginating (applies to each sub-array individually) |

