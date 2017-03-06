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
| contentType        | String                                   | The content type                         |
| requestId          | Integer                                  | The request identifier                   |
| previewContentType | String                                   | (Required with video) The preview content type |
| metadata           | Object { lat: double, lon: double, createdAt: Date } | (Optional) additional metadata about the attached media. Date is an ISO 8601 String. All subfields are optional. |

