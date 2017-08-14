# Translate 

## Get a set of translations 

```shell
curl -X POST -H "Authorization: <AUTHORIZATION_TOKEN>" -H "Content-Type: application/json" -d '[{
  "type": "response",
  "id": "102374",
  "text": "The iron throne"
}, {
	"type": "comment",
	"id": "b95053c3-0de3-468c-b0ec-d9621a850eb6",
	"text": "Haha exactly what I expected"
}]' "https://node.ucic.vc/api/v04/translate/pl"
```

```javascript

```

> The above command returns a 200 success code along with a json response like:

```json
[
    {
        "type": "response",
        "id": "102374",
        "text": "Żelazny tron"
    },
    {
        "type": "comment",
        "id": "b95053c3-0de3-468c-b0ec-d9621a850eb6",
        "text": "Haha dokładnie to, czego się spodziewałem"
    }
]
```

This endpoint lets the client request a set of translations for various items in the platform. The client includes the text to translate along with the type and identifier of the parent entity in order for the server to cache the result and be able to re-use it in the future to minimize calls to the google translate api. Note that the structure of the data the client must POST is identical to the structure that is returned (though of course the text is translated on the way back).

### Which id?

**Comments**  
Use the uuid `.id`  property of the Comment object.  

**Request**  
Use the numeric `.requestId` property from the Request object.  

**Response**  
Use the numeric `.response.id` property of the Card object.   

**Question**   

Use the uuid `.questionId` property of the question-based Theme, or of the Request object.  

**Message**  

Use the numeric `.MI` property of the Message object  

**Tag**  

Use the uuid `.id` property of the Tag object



### HTTP Request

`POST https://node.ucic.vc/api/v04/translate/:language`

### URL Parameters  

| Parameter | Type   | Description                              |
| --------- | ------ | ---------------------------------------- |
| language  | String | The 2 letter iso code for the target language to translate to. |

### Body Parameters

**Note:** body is an array of objects. Object properties are described in the table below  

| Parameter | Type   | Description                              |
| --------- | ------ | ---------------------------------------- |
| type      | String | What type of item is being translated. Currently supports `comment`, `request`, `response`, `question`, `message`, `tag` |
| id        | String | The unique identifier of the entity being translated |
| text      | String | The text to translate                    |

