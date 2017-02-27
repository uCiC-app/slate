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
    "category":    "ucic",
    "translation": "Comment est le coucher du soleil l?-bas?"
  }
]
```

This endpoint retrieves categorized questions.

####Dynamic Questions
The 'dynamic' category of questions attempts to pull in data sources for the askee's location (and any other contextual information added later) to build more customized suggested questions. Note that if using the dynamic category, the lat and lon url parameters become required.

### HTTP Request

`GET https://node.ucic.vc/api/v04/questions`

### Url Parameters

| Parameter | Type   | Description                              |
| --------- | ------ | ---------------------------------------- |
| lang      | String | UTF8 Language Code.  Default is 'en'     |
| category  | String | Category of request, valid categories are ['ucic', 'intro2', 'dynamic'].  Default is 'ucic' |
| lat       | Double | latitude coord of askee (required if category is 'dynamic', ignored otherwise) |
| lon       | Double | longitude coord of askee (required if category is 'dynamic', ignored otherwise) |

