# Branch Deep Links

Branch deep links may be generated via the mobile clients, the uCiC API service, or via the Branch browser dashboard. When clicked on a mobile client, the links will route the user to the app (optionally, via the Play/App Store to install) and pass some metadata to the app contained in the link, indicating how the app should react.

Branch links contain a lot of metadata, but most importantly for client handling, they contain a dictionary of key/value pairs as the `data` object. The `data.type` field will be used by uCiC as the primary key that dictates the intended behaviour of the link.

## External Media Activity Threshold
This link is sent out to twitter users whose media has garnered attention in the uCiC platform in the form of likes and comments.   

```json
{
  "data": {
    "type": "extMediaOutreach",
    "creatorId": "123124194738651",
    "eventId": "2f47f475-97fb-43d6-b432-69836f7fc39c",
    "eventTitle": "This event is best.",
    "itemType": "extMedia",
    "itemId": "tweet_914903140209774592"
  },
  ...
}
```
### Link Behaviour
When clicked, the link should follow the following logic. 

**If a user is already logged in**  
Open the target event room item in the modal popup, similar to how alerts are treated with a means of jumping to the full event room.  

**If user logs in with the link**  
1. During the login process, favour the twitter login option, but still have a means of accessing the default set.
2. Once logged in, open the event room item as above.

**Note:** It is possible for anyone to click the link, whether they be the creator of the media the deep link points to or not. The `data.creatorId` parameter is provided so the client can make this distinction in case the intended behaviour design is updated to perform a different action for the external media's creator vs everyone else. 

