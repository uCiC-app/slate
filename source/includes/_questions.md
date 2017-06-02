# Questions 

## Get questions

```shell
curl "https://node.ucic.vc/api/v04/questions?lang=fr" -H "Authorization: <AUTHORIZATION_TOKEN>"
```

```javascript

```

> The above command returns JSON structured like this:

```json
[
  {
    "id":          "98B69E4B-08DF-4C8F-B10F-1A224CF737BC",
    "question":    "How's the sunset there?",
    "category":    "dynamic",
    "translation": "Comment est le coucher du soleil l?-bas?"
  }
]
```

This endpoint retrieves categorized questions.

####Dynamic Questions
The questions attempt to pull in data sources for the askee's location (and any other contextual information added later) to build more customized suggested questions.

### HTTP Request

`GET https://node.ucic.vc/api/v04/questions`

### Url Parameters

| Parameter | Type    | Description                              |
| --------- | ------- | ---------------------------------------- |
| lang      | String  | UTF8 Language Code.  Default is 'en'     |
| lat       | Double  | latitude coord of askee. Used to populate dynamic quesiton components |
| lon       | Double  | longitude coord of askee. Used to populate dynamic quesiton components |
| category  | String  | Which category of questions to return. Currently supports `'dynamic'` (default), and `'global'`. **Note:** previous categories that have been deprecated will be overridden by 'dynamic' when used. Deprecated categories are: {'ucic', 'intro2', 'onboarding'} |
| limit     | Integer | Maximum number of questions to return (optional). Defaults to 20 |

## Follow a Question

```shell
curl -X GET -H "Authorization: <AUTHORIZATION_TOKEN>" -H "Content-Type: application/json" "https://node.ucic.vc/api/v04/questions/follow/2ef28167-29bd-46bf-851f-c05e2b7e8619" 
```

```javascript

```

> The above command returns 204 on success


This endpoint allows a user to "follow" a question and receive alerts and push notifications when new responses are added to it.

### HTTP Request

`GET https://node.ucic.vc/api/v04/questions/follow/<ID>`

### URL Parameters

| Parameter | Type   | Description                      |
| --------- | ------ | -------------------------------- |
| ID        | String | The id of the question to follow |

## UnFollow a Question

```shell
curl -X GET -H "Authorization: <AUTHORIZATION_TOKEN>" -H "Content-Type: application/json" "https://node.ucic.vc/api/v04/questions/unfollow/2ef28167-29bd-46bf-851f-c05e2b7e8619"  
```

```javascript

```

> The above command returns 204 on success


This endpoint allows a user to stop "following" a question and no longer receive alerts and push notifications when new responses are added to it.

### HTTP Request

`GET https://node.ucic.vc/api/v04/questions/unfollow/<ID>`

### URL Parameters

| Parameter | Type   | Description                        |
| --------- | ------ | ---------------------------------- |
| ID        | String | The id of the question to unfollow |
