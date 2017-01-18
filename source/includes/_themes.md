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
sort | String | Sort of results.  'random' sorts randomly and returns a Sort-Seed header with the random sort seed.  'likes' sorts by likes descending.  Default is sort by likes descending.
seed | UUID | Sorting seed for random sorting.  Returned as header when a random sort is requested

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
curl "https://node.ucic.vc/api/v05/themes/search?query=Boliv" -H "Authorization: <AUTHORIZATION_TOKEN>"
```

```javascript
```

> The above command returns JSON structured like this:

```json
[
  {
    "name": "Bolivia",
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


