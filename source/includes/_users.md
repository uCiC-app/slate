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

| Parameter   | Type    | Description                              |
| ----------- | ------- | ---------------------------------------- |
| address     | String  | (Optional) The user's address            |
| deviceId    | UUID    | Device identifier                        |
| email       | String  | The user's email address                 |
| legacyToken | String  | (Optional)  The existing V1 app authorization token.  If present, the fid is linked to the owner of this provided legacy token rather than creating a new user in the database |
| os          | Integer | Device operating system.  0 for iOS, 1 for Android (This is largely deprecated, replaced by the user-agent header.  However, some obscure parts of the system still make use of it) |
| photoURL    | String  | (Optional) Publically accessible path to an avatar photo for the user |
| pushId      | String  | (Optional) Firebase (FCM) Push ID        |
| token       | String  | (Optional) The signed firebase token containing a firebase id (fid).  Required for firebase logins |
| username    | String  | The user's desired username              |
| category    | String  | (Optional) The login category.  Currently only 'guest' is supported |

### Errors
| Error | Meaning                               |
| ----- | ------------------------------------- |
| 401   | Unauthorized, login has been rejected |
| 730   | User has been deleted                 |
| 844   | Account is locked                     |


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

##Geo

```shell
curl -X POST "https://node.ucic.vc/api/v04/users/geo"
```
```javascript

```

> The above command returns a 200 success status


This endpoint allows the client to update the server with important information about it's state. The enpoint accepts and updates the location, time zone and push ID of the client.


### HTTP Request

`POST https://node.ucic.vc/api/v04/users/geo`

### Request Body

| Parameter       | Type         | Description                              |
| --------------- | ------------ | ---------------------------------------- |
| location        | { lat, lon } | Floating point numbers representing the client's location |
| timeZoneMinutes | Integer      | The client's current offset from UTC in minutes. (Ex. Eastern Time is UTC -5 hours which is -300 minutes.) |
| pushId          | String       | (Optional) The client's key for receiving remote push notifications |
| country         | String       | (Optional) The client's current country of location |

### Errors
| Error | Meaning                                  |
| ----- | ---------------------------------------- |
| 400   | Bad request; missing lat, lon, or timeZoneMinutes |
| 401   | Unauthorized, authorization token was rejected |
| 500   | Server encountered an error              |

##Get
```shell
curl -X GET "https://node.ucic.vc/api/v04/users/414559"
```
```javascript

```
> A successful call will return a user's profile information in the format:

```json
{
  "avatar": "https://media.ucic.vc/media/default/thumb.jpg",
  "createdAt": "2017-05-18T21:32:11.000Z",
  "fullname": "Samsung",
  "tagLine": "A Samsung test device on Jan's desk.",
  "rating": 5,
  "id": "414559",
  "lat": 43.4507874,
  "lon": -80.4983869,
  "likes": 100,
  "responseCount": 0,
  "completedRequests": 0,
  "timeZoneMinutes": -240,
  "youFollowUser": true,
  "userFollowsYou": false,
  "userFollowCount": 2,
  "followUserCount": 1,
  "canChat": true
}

```
This endpoint provides a means of retrieving the profile information for a given user Id. 

### HTTP Request

`GET https://node.ucic.vc/api/v04/users/:id`

### URL Parameters
| Parameter | Type    | Description                              |
| --------- | ------- | ---------------------------------------- |
| id        | Integer | The user Id of the user to retrieve the profile for |


##Set

```shell
curl -X POST "https://node.ucic.vc/api/v04/users/set"
```
```javascript

```
> The above command returns a 200 success status along with the updated values of the changed fields
> Note: the response will contain only the field(s) that were modified by the request, since all of the fields are optional.

```json
{
  "visibleLocation": "1",
  "username": "BillyJean",
  "avatar": "http://media.ucic.vc/media/427F0DC4-B2B6-4182-8088-D31BB5CB0934/thumb.jpg",
  "email": "not@mylov.er",
  "tagLine": "Not my Lover."
}
```

This endpoint allows the clients to update user information. Specifically, the map visibility status, avatar, email, tagline, and username may be changed with this route.

### HTTP Request

`POST https://node.ucic.vc/api/v04/users/set`

### Request Body

| Parameter       | Type       | Description                              |
| --------------- | ---------- | ---------------------------------------- |
| visibleLocation | Int {0, 1} | (Optional\*) Integer representing the desired map visibility for the user, where 1 represents a public profile and 0 a private one. Note: the v03/settings/get route will return the inverse integer for legacy reasons (0 for public, 1 for private) |
| username        | String     | (Optional\*) The new string to update the username to. |
| avatarBuffer    | String     | (Optional\*) The base 64 encoded image buffer representing the image to change the user's avatar to. |
| email           | String     | (Optional\*) The new email to set for the user. |
| tagLine         | String     | (Optional\*) A short bio for the user's profile. Up to 255 characters, an error will be returned if this limit is not respected. |

\*Note: though all five parameters are optional, **at least one must be sent** with the call, or a 400 error message will be returned.

### Errors
| Error | Meaning                                  |
| ----- | ---------------------------------------- |
| 400   | Bad request; Either no recognized parameters were sent, or invalid values for at least one that was. |
| 401   | Unauthorized, authorization token was rejected |
| 500   | Server encountered an error              |



## Follow User

```shell
curl -X GET -H "Authorization: <AUTHORIZATION_TOKEN>" "https://node.ucic.vc/api/v04/users/follow/:id"
```
> The above command returns a 204 success status

```json

```
Follow the user specified by the url id param to subscribe to notification for their activity.

### HTTP Request

`GET https://node.ucic.vc/api/v04/users/follow/:id`

### URL Params
| param | Type    | Description                  |
| ----- | ------- | ---------------------------- |
| id    | Integer | The id of the user to follow |

### Errors
| Error | Meaning                               |
| ----- | ------------------------------------- |
| 400   | Bad request; Attempted to follow self |

## Unfollow User

```shell
curl -X GET -H "Authorization: <AUTHORIZATION_TOKEN>" "https://node.ucic.vc/api/v04/users/unfollow/:id"
```
> The above command returns a 204 success status

```json

```
Stop following the user specified by the url id param to no longer receive notifications for their activity.

### HTTP Request

`GET https://node.ucic.vc/api/v04/users/follow/:id`

### URL Params
| param | Type    | Description                    |
| ----- | ------- | ------------------------------ |
| id    | Integer | The id of the user to unfollow |

### Errors
| Error | Meaning                                 |
| ----- | --------------------------------------- |
| 400   | Bad request; Attempted to unfollow self |

## User's Followers

```shell
curl -X GET -H "Authorization: <AUTHORIZATION_TOKEN>" "https://node.ucic.vc/api/v04/users/followers/:id"
```
> The above command returns a 200 success status along with a json response like:

```json
[
    {
        "id": 195685,
        "avatar": "https://media.ucic.vc/media/4A0F0DEA-16E9-49E0-B3C0-5AC38FD759E8/thumb.jpg",
        "username": "Khan",
        "likes": 114,
        "youFollow": false
    },
    ...
]

```
Returns an array of the users that follow the user specified by the url id param.

### HTTP Request

`GET https://node.ucic.vc/api/v04/users/followers/:id`

### URL Params
| param | Type    | Description                              |
| ----- | ------- | ---------------------------------------- |
| id    | Integer | The id of the user whose followers with be returned |

### Query Params
| param | Type    | Description                              |
| ----- | ------- | ---------------------------------------- |
| limit    | Integer | Maximum number of followers to return |
| offset    | Integer | Offset in the list of followers to start return from |

## User's Following

```shell
curl -X GET -H "Authorization: <AUTHORIZATION_TOKEN>" "https://node.ucic.vc/api/v04/users/following/:id"
```
> The above command returns a 200 success status along with a json response like:

```json
[
    {
        "id": 195685,
        "avatar": "https://media.ucic.vc/media/4A0F0DEA-16E9-49E0-B3C0-5AC38FD759E8/thumb.jpg",
        "username": "Khan",
        "likes": 114,
        "youFollow": false
    },
    ...
]

```
Returns an array of the users that the user specified by the url id param follows.

### HTTP Request

`GET https://node.ucic.vc/api/v04/users/followers/:id`

### URL Params
| param | Type    | Description                              |
| ----- | ------- | ---------------------------------------- |
| id    | Integer | The id of the user whose following users with be returned |

### Query Params
| param | Type    | Description                              |
| ----- | ------- | ---------------------------------------- |
| limit    | Integer | Maximum number of followers to return |
| offset    | Integer | Offset in the list of followers to start return from |


##Unseen Items

```shell
curl -X GET -H "Authorization: <AUTHORIZATION_TOKEN>" "https://node.ucic.vc/api/v04/users/unseenCounts"
```
> The above command returns a 200 success status along with a response body structured as shown:

```json
{
  "unseenEvents": 1,
  "unseenConversations": 5,
  "unseenDirectRequests": 1,
  "unseenGlobalRequests": 10
}
```
This route returns the itemized counts of various items in the app that the user's client has not yet marked as seen. 

### HTTP Request

`GET https://node.ucic.vc/api/v04/users/unseenCounts`

##Logout

```shell
curl -X GET -H "Authorization: <AUTHORIZATION_TOKEN>" "https://node.ucic.vc/api/v04/users/logout"
```

> The above command returns a 204 success status


This endpoint is used to notify the service that the user has logged out of the uCiC client. This removes the user from the world map and prevents the server sending push notifications to this device until a user logs in on it again.


### HTTP Request

`GET https://node.ucic.vc/api/v04/users/logout`

The token in the "Authorization" header is used to determine the user to log out.