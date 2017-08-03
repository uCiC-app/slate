# Responses 

## Create a Response

```shell
curl -X POST -H "Authorization: <AUTHORIZATION_TOKEN>" -H "Content-Type: multipart/form-data; boundary=----WebKitFormBoundary7MA4YWxkTrZu0gW" -F "files=@/Users/recurrence/Downloads/misc/SampleVideo_1280x720_1mb.mp4" -F "files=@/Users/recurrence/Downloads/demo-image.jpg" -F "video={"RI": 45220%2C"PContentType":"png"%2C"ContentType":"mp4"%2C "Caption":"A pretty dog video!"}" "https://node.ucic.vc/api/v04/responses"
```
```javascript
var http = require("https");

var options = {
  "method": "POST",
  "hostname": "node.ucic.vc",
  "port": null,
  "path": "/api/v04/responses",
  "headers": {
    "content-type": "multipart/form-data; boundary=----WebKitFormBoundary7MA4YWxkTrZu0gW",
    "authorization": <AUTHORIZATION_TOKEN>,
  }
};

var req = http.request(options, function (res) {
  var chunks = [];

  res.on("data", function (chunk) {
    chunks.push(chunk);
  });

  res.on("end", function () {
    var body = Buffer.concat(chunks);
    console.log(body.toString());
  });
});

req.write("------WebKitFormBoundary7MA4YWxkTrZu0gW\r\nContent-Disposition: form-data; name=\"image\"; filename=\"12471697_10101450624474947_1564349885388828867_o.jpg\"\r\nContent-Type: image/jpeg\r\n\r\n\r\n------WebKitFormBoundary7MA4YWxkTrZu0gW\r\nContent-Disposition: form-data; name=\"video\"\r\n\r\n\r\n------WebKitFormBoundary7MA4YWxkTrZu0gW\r\nContent-Disposition: form-data; name=\"caption\"\r\n\r\n\"New Hi There!\"\r\n------WebKitFormBoundary7MA4YWxkTrZu0gW\r\nContent-Disposition: form-data; name=\"contentType\"\r\n\r\njpg\r\n------WebKitFormBoundary7MA4YWxkTrZu0gW\r\nContent-Disposition: form-data; name=\"requestId\"\r\n\r\n45220\r\n------WebKitFormBoundary7MA4YWxkTrZu0gW\r\nContent-Disposition: form-data; name=\"previewContentType\"\r\n\r\npng\r\n------WebKitFormBoundary7MA4YWxkTrZu0gW--");
req.end();
```
```swift
import Foundation

let headers = [
  "content-type": "multipart/form-data; boundary=----WebKitFormBoundary7MA4YWxkTrZu0gW",
  "authorization": <AUTHORIZATION_TOKEN>,
]
let parameters = [
  [
    "name": "image",
    "fileName": "/Users/recurrence/Downloads/12471697_10101450624474947_1564349885388828867_o.jpg"
  ],
  [
    "name": "video",
    "fileName": ""
  ],
  [
    "name": "caption",
    "value": "\"New Hi There!\""
  ],
  [
    "name": "contentType",
    "value": "jpg"
  ],
  [
    "name": "requestId",
    "value": "45220"
  ],
  [
    "name": "previewContentType",
    "value": "png"
  ]
]

let boundary = "----WebKitFormBoundary7MA4YWxkTrZu0gW"

var body = ""
var error: NSError? = nil
for param in parameters {
  let paramName = param["name"]!
  body += "--\(boundary)\r\n"
  body += "Content-Disposition:form-data; name=\"\(paramName)\""
  if let filename = param["fileName"] {
    let contentType = param["content-type"]!
    let fileContent = String(contentsOfFile: filename, encoding: String.Encoding.utf8)
    if (error != nil) {
      print(error)
    }
    body += "; filename=\"\(filename)\"\r\n"
    body += "Content-Type: \(contentType)\r\n\r\n"
    body += fileContent
  } else if let paramValue = param["value"] {
    body += "\r\n\r\n\(paramValue)"
  }
}

let request = NSMutableURLRequest(url: NSURL(string: "https://node.ucic.vc/api/v04/responses")! as URL,
                                        cachePolicy: .useProtocolCachePolicy,
                                    timeoutInterval: 10.0)
request.httpMethod = "POST"
request.allHTTPHeaderFields = headers
request.httpBody = postData as Data

let session = URLSession.shared
let dataTask = session.dataTask(with: request as URLRequest, completionHandler: { (data, response, error) -> Void in
  if (error != nil) {
    print(error)
  } else {
    let httpResponse = response as? HTTPURLResponse
    print(httpResponse)
  }
})

dataTask.resume()
```
```java
OkHttpClient client = new OkHttpClient();

MediaType mediaType = MediaType.parse("multipart/form-data; boundary=----WebKitFormBoundary7MA4YWxkTrZu0gW");
RequestBody body = RequestBody.create(mediaType, "------WebKitFormBoundary7MA4YWxkTrZu0gW\r\nContent-Disposition: form-data; name=\"image\"; filename=\"12471697_10101450624474947_1564349885388828867_o.jpg\"\r\nContent-Type: image/jpeg\r\n\r\n\r\n------WebKitFormBoundary7MA4YWxkTrZu0gW\r\nContent-Disposition: form-data; name=\"video\"\r\n\r\n\r\n------WebKitFormBoundary7MA4YWxkTrZu0gW\r\nContent-Disposition: form-data; name=\"caption\"\r\n\r\n\"New Hi There!\"\r\n------WebKitFormBoundary7MA4YWxkTrZu0gW\r\nContent-Disposition: form-data; name=\"contentType\"\r\n\r\njpg\r\n------WebKitFormBoundary7MA4YWxkTrZu0gW\r\nContent-Disposition: form-data; name=\"requestId\"\r\n\r\n45220\r\n------WebKitFormBoundary7MA4YWxkTrZu0gW\r\nContent-Disposition: form-data; name=\"previewContentType\"\r\n\r\npng\r\n------WebKitFormBoundary7MA4YWxkTrZu0gW--");
Request request = new Request.Builder()
  .url("https://node.ucic.vc/api/v04/responses")
  .post(body)
  .addHeader("content-type", "multipart/form-data; boundary=----WebKitFormBoundary7MA4YWxkTrZu0gW")
  .addHeader("authorization", <AUTHORIZATION_TOKEN>)
  .build();

Response response = client.newCall(request).execute();
```

> The above command returns Created 201:

This endpoint creates a response for a request.

**Note:** When creating a text-only response, use the `caption` field as the text response content and send `contentType` field with the string value `"text"`;

**Note:** The `metadata.uploaded` integer flag is used to distinguish captured (0) vs attached (1) media in the response. If not provided, the server will assume the media was captured, unless one of the other metadata fields are provided, which implicitly indicates that the media is attached.

### Uploading a response to an Event Room
Event rooms may contain "free floating" media objects. In order to create these, perform a normal response upload, but as the `requestId` body param, provide the ID of the event room, prefixed with `event_`. So if the event room ID is `1GJpe5m8X8Q9`, the requestId will be `event_1GJpe5m8X8Q9` in the body.

### Uploading to S3 Directly
The service now supports letting the clients upload the video file to S3 directly to free up uCiC serivce's bandwidth and processing power for other work. In order to upload from the client to the S3 bucket, you will need to use a TransferUtility ([Android](https://docs.aws.amazon.com/mobile/sdkforandroid/developerguide/s3transferutility.html), [iOS](https://docs.aws.amazon.com/mobile/sdkforios/developerguide/s3transferutility.html)) properly configured to point to the US-WEST-2 region and identifying itself using the predefined key to be allowed write access (Note, this key is not posted here as these docs are public). 

**Note:** By default, the Transfer Utility does not allow public read of the uploaded files. Make sure you pass the `PublicRead` argument to the .upload method when called to ensure clients can later view the media.

When calling the TansferUtility .upload method, use the following arguments: 

`bucketName = "ucic-production"`  
`key = "media/videoId/original.mp4"`

**VideoId Generation**  
The videoId must be a unique String of length up to 36 characters. Use the following method to generate the key: 

`videoId = platformInitial + "_" + userId + "_" + unixTimestamp`

where  

 `platformInitial` is "B" for iOS and "A" for Android

`userId` is the numerical ID of the logged in user

`unixTimestamp` is the 13 digit unit timestamp expressed in milliseconds.

The resulting videoId should look soething like `A_414695_1499280905159`


### HTTP Request

`POST https://node.ucic.vc/api/v04/responses`

### Multi-Part Parameters
| Parameter | Type | Description                              |
| --------- | ---- | ---------------------------------------- |
| image     | File | The response image (Preview if video provided) |
| video     | File | The response video                       |

### Request Body

| Parameter          | Type                                     | Description                              |
| ------------------ | ---------------------------------------- | ---------------------------------------- |
| caption            | String                                   | The response caption                     |
| videoId            | String                                   | If the client has already uploaded the video file to the S3 bucket, pass this param instead of the video file. This is the id of the media object in the S3 bucket,  where the path to the object is `"ucic-production/media/{videoId}/original.mp4"` (see **videoId Generation** above in the **Uploading to S3 Directly** section above for more details) |
| contentType        | String                                   | (required) The content type (Either the file extension or the string 'text' for text-only responses) |
| requestId          | Integer                                  | The request identifier                   |
| previewContentType | String                                   | (Required with video) The preview content type |
| questionId         | String                                   | (Optional) The id of the question associated with the request. |
| metadata           | Object { lat: double, lon: double, createdAt: Date, uploaded: Integer } | Additional metadata about the media. Date is an ISO 8601 String. All subfields are optional. The `uploaded` field tells the server if the client captured the media during the response flow (`uploaded: 0`) or attached an existing piece of media (`uploaded:1`). |

