# Questions 

## Get set of questions

```shell

curl "https://node.ucic.vc/api/v04/questions?lang=fr"
  -H "Authorization: <AUTHORIZATION_TOKEN>"
```

```javascript
```

> The above command returns JSON structured like this:

```json
[
  {
    "id":          "98B69E4B-08DF-4C8F-B10F-1A224CF737BC",
    "question":    "How's the sunset there?",
    "category":    "ucic",
    "askCounter":  0,
    "translation": "Comment est le coucher du soleil l?-bas?"
  }
]
```

This endpoint retrieves the current user's events.

### HTTP Request

`GET https://node.ucic.vc/api/v04/questions`

### Url Parameters

Parameter | Type | Description
--------- | ---- | -----------
lang | String | UTF8 Language Code
category | String | Category of request, valid categories are ['ucic', 'onboarding']
limit | Unsigned Integer | Maximum number of comments to return
offset | Unsigned Integer | Offset in list of commentss to start return from
page | Unsigned Integer | Page of comments to return

