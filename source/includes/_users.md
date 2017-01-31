# Users

## Login

```shell
curl -X POST -H "Content-Type: application/json" -d '{ "token": "df976sdf9sd6ff6g679adfg59fdg995df8ag697dfg694daf9g96adfg96", "os": 0, "pushId": "kjsfgsadgf899ya7w4bv7b4b4tvhhbt4va0b4vbva9b34c4b8g6438bcgc4", "photoURL": "https://myAvatar.com/media/avatar.png", "email": "somebody@whoknows.com", "address": "233 Bucksville, Atlanta, Georgia United States 30309", "username": "Dude DaDuder" }' "https://node.ucic.vc/api/v04/users/login"


```
```javascript
```

> The above command returns the current authorization token as well as the user object:

```json
{
  "session": "DEC604AC-C29F-4764-B9C6-2CEC7351ABB6",
  "user": { // User Object }
}
```

This endpoint logs in a user.  It creates the user in the database if the fid is not found.  The endpoint will alternatively link an existing legacy app token with a fid if one is provided.

### HTTP Request

`POST https://node.ucic.vc/api/v04/users/login`

### Request Body

Parameter | Type | Description
--------- | ---- | -----------
address | String | (Optional) The user's address
deviceId | UUID | Device identifier
email | String | The user's email address
legacyToken | String | (Optional)  The existing V1 app authorization token.  If present, the fid is linked to the owner of this provided legacy token rather than creating a new user in the database
os | Integer | Device operating system.  0 for iOS, 1 for Android (This is largely deprecated, replaced by the user-agent header.  However, some obscure parts of the system still make use of it)
photoURL | String | (Optional) Publically accessible path to an avatar photo for the user
pushId | String | (Optional) Firebase (FCM) Push ID
token | String | The signed firebase token containing a firebase id (fid)
username | String | The user's desired username

### Errors
Error | Meaning
---------- | -------
401 | Unauthorized, login has been rejected
730 | User has been deleted
844 | Account is locked


## Block

```shell
curl -X POST "https://node.ucic.vc/api/v04/users/132406/block"
```
```javascript
```

> The above command returns a 204 success status


This endpoint blocks a user.


### HTTP Request

`POST https://node.ucic.vc/api/v04/users/:id/block`

