# Mobile

## Get Minimum and Latest App Versions

```shell
curl "https://node.ucic.vc/api/v04/mobile/versions"  -H "Authorization: <AUTHORIZATION_TOKEN>"
```
```javascript

```

> The above command returns JSON structured like this:

```json

{
  "minVersion": "2.0",
  "latestVersion": "2.7"
}

```

This endpoint retrieves the current latest and minimum supported app versions for the requesting client. 

### HTTP Request

`GET https://node.ucic.vc/api/v04/mobile/versions`

### Errors

| Code | Error   | Description           |
| --------- | ------ | --------------------- |
| 400      | UNSUPPORTED_USER_AGENT | The user-agent string sent with the request does not match a recognized uCiC Mobile Client |