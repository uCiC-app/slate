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
| FI          | String  | (Optional) Facebook Identifier for Firebase User |
| GI          | String  | (Optional) Google Identifier for Firebase User |
| TI          | String  | (Optional) Twitter Identifier for Firebase User |
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
  "badge": "https://media.ucic.vc/assets/tags/CA.png",
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
        "fullname": "Khan",
        "likes": 114,
        "youFollowUser": false,
        "badge": "https://media.ucic.vc/assets/tags/CA.png"
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
| param  | Type    | Description                              |
| ------ | ------- | ---------------------------------------- |
| limit  | Integer | Maximum number of followers to return    |
| offset | Integer | Offset in the list of followers to start return from |

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
        "fullname": "Khan",
        "likes": 114,
        "youFollowUser": false,
        "badge": "https://media.ucic.vc/assets/tags/CA.png"
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
| param  | Type    | Description                              |
| ------ | ------- | ---------------------------------------- |
| limit  | Integer | Maximum number of followers to return    |
| offset | Integer | Offset in the list of followers to start return from |

## Media

```shell
curl -X GET -H "Authorization: <AUTHORIZATION_TOKEN>" "https://node.ucic.vc/api/v04/users/media/:userId/:type"
```
> The above command returns a 200 success status along with a json response like:

```json
[{
  "request": {
    "id": "300964",
    "createdAt": "2017-10-07T17:00:00.000Z",
    "text": "8th Annual Under the Big Sky Buddy Walk®",
    "likeCount": 0,
    "liked": false,
    "creator": {
      "userId": 194673,
      "userName": "Hyeon-Ju Kim",
      "userAvatar": "https://media.ucic.vc/media/416C5EA4-E6B5-4532-9DC3-E7392E397B31/thumb.jpg",
      "badge": null
    }
  },
  "response": {
    "cardId": "72F7D8EF-B5B3-455D-8047-413FE89B8080",
    "MI": "76166",
    "text": "content",
    "likeCount": 1,
    "liked": false,
    "commentCount": 0,
    "createdAt": "2017-10-12T16:46:04.000Z",
    "mimeType": "image/jpeg",
    "url": "https://media.ucic.vc/media/72F7D8EF-B5B3-455D-8047-413FE89B8080/original.jpg",
    "thumb": "https://media.ucic.vc/media/72F7D8EF-B5B3-455D-8047-413FE89B8080/thumb.jpg",
    "display": "https://media.ucic.vc/media/72F7D8EF-B5B3-455D-8047-413FE89B8080/display.jpg",
    "creator": {
      "userId": 195685,
      "userName": "Khan",
      "userAvatar": "https://media.ucic.vc/media/4A0F0DEA-16E9-49E0-B3C0-5AC38FD759E8/thumb.jpg",
      "badge": "https://media.ucic.vc/assets/tags/CA.png"
    }
  }
}]
```
Returns an array of the media that the specified user has sent or received.

### HTTP Request

`GET https://node.ucic.vc/api/v04/users/media/:userId/:type`

### URL Params
| param  | Type    | Description                              |
| ------ | ------- | ---------------------------------------- |
| userId | Integer | The id of the user whose related media to return |
| type   | String  | currently only supports `sent` and `received` |

### Query Params
| param  | Type    | Description                              |
| ------ | ------- | ---------------------------------------- |
| limit  | Integer | Maximum number of media to return        |
| offset | Integer | Offset in the list of media to start return from |

##User Trophies
```shell
curl -X GET -H "Authorization: <AUTHORIZATION_TOKEN>" "https://node.ucic.vc/api/v04/user/awards/trophies/195685"
```
> The above command returns a 200 success status along with a json response like:

```json
[{
  "id": "4A0F0DEA-16E9-49E0-B3C0-5AC38FD759E8",
  "UI": 195685,
  "type": "ucicDev",
  "date": "2017-01-09T12:45:50.000Z",
  "name": "uCiC Developer",
  "icon": "https://media.ucic.vc/trophy/ucic_dev.png",
  "description": "Denotes the users directly involved in the development of the uCiC platform."
}]
```
Returns an array of the trophies the given user has earned.

### HTTP Request

`GET https://node.ucic.vc/api/v04/user/awards/trophies/:ui`

### URL Params
| param | Type    | Description                              |
| ----- | ------- | ---------------------------------------- |
| ui    | Integer | The id of the user whose trophies to return |

### Query Params
| param  | Type    | Description                              |
| ------ | ------- | ---------------------------------------- |
| limit  | Integer | Maximum number of trophies to return     |
| offset | Integer | Offset in the list of trophies to start return from |

##User Stamps
```shell
curl -X GET -H "Authorization: <AUTHORIZATION_TOKEN>" "https://node.ucic.vc/api/v04/user/awards/stamps/195685"
```
> The above command returns a 200 success status along with a json response like:

```json
[{
  "id": "4A0F0DEA-16E9-49E0-B3C0-5AC38FD759E8",
  "UI": 195685,
  "type": "remote",
  "date": "2017-01-09T12:45:50.000Z",
  "eventId": "1234567890",
  "eventName": "The Best Test Event",
  "thumb": null
}]
```
Returns an array of the stamps the given user has earned.

### HTTP Request

`GET https://node.ucic.vc/api/v04/user/awards/stamps/:ui`

### URL Params
| param | Type    | Description                              |
| ----- | ------- | ---------------------------------------- |
| ui    | Integer | The id of the user whose stamps to return |

### Query Params
| param  | Type    | Description                              |
| ------ | ------- | ---------------------------------------- |
| limit  | Integer | Maximum number of stamps to return     |
| offset | Integer | Offset in the list of stamps to start return from |

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

## List Facebook Friends
```shell
curl -X POST -H "Content-Type: application/json" -d '{ "FI": ["167217543790267", "237747386665479", "1942446369318771"] }' "https://node.ucic.vc/api/v04/user/fbFriends"
```
> The route returns an array of JSON user objects with the format:   

  

```json
[{
  "id": "414624",
  "avatar": "https://media.ucic.vc/media/default/thumb.jpg",
  "fullname": "Spock",
  "tagLine": "Live long and prosper",
  "likes": 0,
  "youFollowUser": false,
  "badge": "https://media.ucic.vc/assets/tags/CA.png"
}]
```

This route accepts an array of Facebook Ids (as strings) and returns a list of any existing uCiC users who are in the array (ie. Facebook friends of the requesting user).

### HTTP Request

`POST https://node.ucic.vc/api/v04/user/fbFriends`

### Body Params
| param | Type         | Description                              |
| ----- | ------------ | ---------------------------------------- |
| FI    | String Array | The array of FI identifying the friends of the requesting user to match against existing uCiC users. |

## List Twitter Friends
```shell
curl -X POST -H "Content-Type: application/json" -d '{ "followerTIs": ["167217543790267", "237747386665479"], "followingTIs": [] }' "https://node.ucic.vc/api/v04/user/twFriends"
```
> The route returns an array of JSON user objects with the format:   


```json
[{
  "id": "414846",
  "avatar": "https://media.ucic.vc/media/455535F4-B570-431A-B120-34D085932427/thumb.jpg",
  "fullname": "TwitterJan",
  "tagLine": "an tagline",
  "likes": 1,
  "youFollowUser": false,
  "twitterFollowState": "follower",
  "badge": "https://media.ucic.vc/assets/tags/CA.png"
}]
```

This route accepts 2 arrays of Twitter user Ids (as strings) and returns a list of any existing uCiC users who are in the arrays (ie. followers/following Twitter users of the requesting user). Note: the `twitterFollowState` indicates what the twitter relationship of the user is relative to the requesting user. Possible values are `follower`, `following`, and `both`.

### HTTP Request

`POST https://node.ucic.vc/api/v04/user/twFriends`

### Body Params
| param        | Type         | Description                              |
| ------------ | ------------ | ---------------------------------------- |
| followerTIs  | String Array | The array of TI identifying the followers of the requesting user to match against existing uCiC users. |
| followingTIs | String Array | The array of TI identifying the following users of the requesting user to match against existing uCiC users. |

## Followee Suggestions
```shell
curl -X GET -H "Authorization: <AUTHORIZATION_TOKEN>" "https://node.ucic.vc/api/v04/users/followSuggestions"
```
> The route returns an array of JSON user objects with the format:   


```json
[{
  "id": "414844",
  "avatar": "https://media.ucic.vc/media/A6C7B115-96CB-4300-A976-D9C3C8EC0CE8/thumb.jpg",
  "fullname": "Sarah",
  "tagLine": null,
  "likes": 2,
  "youFollowUser": false,
  "badge": "https://media.ucic.vc/assets/tags/CA.png"
}]
```

This route returns an array of potential users to follow. It is a mix of the 5 most recent users and the 5 users who most recently posted media with the constraints:
- not already followed
- follow candidates must have avatar set
- unique across the 2 categories
- media was not reported by the querying user (applied to most recet media users only)

### HTTP Request

`GET https://node.ucic.vc/api/v04/user/followSuggestions`


##Logout

```shell
curl -X GET -H "Authorization: <AUTHORIZATION_TOKEN>" "https://node.ucic.vc/api/v04/users/logout"
```

> The above command returns a 204 success status


This endpoint is used to notify the service that the user has logged out of the uCiC client. This removes the user from the world map and prevents the server sending push notifications to this device until a user logs in on it again.


### HTTP Request

`GET https://node.ucic.vc/api/v04/users/logout`

The token in the "Authorization" header is used to determine the user to log out.