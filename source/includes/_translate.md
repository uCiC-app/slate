# Translate 

## Get a set of translations 

```shell
curl -X POST -H "Authorization: <AUTHORIZATION_TOKEN>" -H "Content-Type: application/json" -d '["hello", "going to send this text"]' "https://node.ucic.vc/api/v04/translate/pl"
```

```javascript

```

> The above command returns a 200 success code along with a json response like:

```json
[
    "cześć",
    "Zamierza wysłać ten tekst"
]
```

This endpoint lets the client request a set of translations for arbitrary text. The client sends an array of strings to be translated and the server responds with a translated string array in the same order.

### HTTP Request

`POST https://node.ucic.vc/api/v04/translate/:language`

### URL Parameters  

| Parameter | Type   | Description                              |
| --------- | ------ | ---------------------------------------- |
| language  | String | The 2 letter iso code for the target language to translate to. |

### Body Parameters

Body is an array of strings


