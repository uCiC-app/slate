#Themes 

## Get All Themes 

```shell
curl "https://node.ucic.vc/api/v05/themes/get" -H "Authorization: <AUTHORIZATION_TOKEN>"
```

```javascript
```

> The above command returns JSON structured like this:

```json
[
  {
    "id": "E73CD7C4-35E7-4A37-9850-950E22B2BCCF",
    "name": "United States of America",
    "maxLikes": "78",
    "logo": "http://staging-media.ucic.vc/assets/tags/US.png"
  }
]
```

This endpoint retrieves all themes.

### HTTP Request

`GET https://node.ucic.vc/api/v05/themes`

### Query Parameters

Parameter | Default | Description
--------- | ------- | -----------
limit | Unsigned Integer | Maximum number of themes to return
offset | Unsigned Integer | Offset in list of themes to start return from
page | Unsigned Integer | Page of themes to return

<aside class="success">
Remember — a happy uCiC client is an authenticated uCiC client!
</aside>

## Get a Specific Theme 

```shell
curl "https://node.ucic.vc/api/v05/themes/928CF4AC-A5BF-4A8B-8C47-62E58AE1F655" -H "Authorization: <AUTHORIZATION_TOKEN>"
```

```javascript
```

> The above command returns JSON structured like this:

```json
{
  "id": "928CF4AC-A5BF-4A8B-8C47-62E58AE1F655",
  "name": "Canada",
  "maxLikes": "28",
  "logo": "http://staging-media.ucic.vc/assets/tags/CA.png"
}
```

This endpoint retrieves a specific theme.

### HTTP Request

`GET https://node.ucic.vc/api/v05/themes/<ID>`

### URL Parameters

Parameter | Type | Description
--------- | ---- | -----------
ID | UUID | The ID of the theme to retrieve

## Search for a Theme 

```shell
curl "https://node.ucic.vc/api/v05/themes/search?query=oliv" -H "Authorization: <AUTHORIZATION_TOKEN>"
```

```javascript
```

> The above command returns JSON structured like this:

```json
[
  {
    "title": "Bolivia",
    "id": "EF60D822-67DB-4E2D-8F01-4B31F54AF21E"
  }
]
```

This endpoint searches for themes matching their title against the provided query.

### HTTP Request

`GET https://node.ucic.vc/api/v05/themes/search?query=<SEARCH_QUERY>`

### Query Parameters

Parameter | Type | Description
--------- | ---- | -----------
query | String | The search substring to find matching themes for 

## Get the Cards for a Theme 

```shell
curl "https://node.ucic.vc/api/v05/themes/928CF4AC-A5BF-4A8B-8C47-62E58AE1F655/cards" -H "Authorization: <AUTHORIZATION_TOKEN>"
```

```javascript
```

> The above command returns JSON structured like this:

```json
[
  {
    "id": "4F211D7B-5DA4-42FA-9C44-E8CEAB4C05EC",
    "tagId": "928CF4AC-A5BF-4A8B-8C47-62E58AE1F655",
    "request": {
      "id": "40839",
      "createdAt": "2016-04-22T01:02:37.000Z",
      "sender": {
        "id": "36001",
        "login": null,
        "fullname": "Jack Liu",
        "email": "jackjack_liu@hotmail.com",
        "avatar": "http://staging-media.ucic.vc/media/default/thumb.png",
        "lat": 48.715,
        "lon": -80.5174639,
        "likes": "10",
        "createdAt": "2016-04-22T01:01:54.446Z"
      },
      "receiver": null,
      "body": "Anything interesting to see around you?",
      "media": null
    },
    "response": {
      "id": "14062",
      "createdAt": "2016-04-22T01:29:23.530Z",
      "sender": {
        "id": "71",
        "login": "uCiC_app",
        "fullname": "Ashley",
        "email": "",
        "avatar": "http://staging-media.ucic.vc/media/default/thumb.png",
        "likes": "10",
        "responses": 84,
        "createdAt": "2014-08-31T18:44:51.156Z"
      },
      "receiver": null,
      "body": "Mural",
      "media": {
        "id": "4F211D7B-5DA4-42FA-9C44-E8CEAB4C05EC",
        "mi": "11831",
        "url": "http://staging-media.ucic.vc/media/4F211D7B-5DA4-42FA-9C44-E8CEAB4C05EC/original.jpg",
        "thumb": "http://staging-media.ucic.vc/media/4F211D7B-5DA4-42FA-9C44-E8CEAB4C05EC/thumb.jpg",
        "lat": 43.4513854980469,
        "lon": -80.498664855957,
        "mimeType": "image/jpeg",
        "likes": 28,
        "liked": false,
        "createdAt": "2016-04-22T01:29:37.000Z",
        "tags": []
      }
    }
  }
]
```

This endpoint retrieves the cards for a theme.

### HTTP Request

`GET https://node.ucic.vc/api/v05/themes/<ID>/cards`

### URL Parameters

Parameter | Type | Description
--------- | ---- | -----------
ID | UUID | The ID of the theme to retrieve cards for

### Query Parameters

Parameter | Type | Description
--------- | ------- | -----------
limit | Unsigned Integer | Maximum number of cards to return
offset | Unsigned Integer | Offset in list of cards to start return from
page | Unsigned Integer | Page of cards to return

