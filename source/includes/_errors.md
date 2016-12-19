# Errors

The Theme API uses the following error codes:


Error Code | Meaning
---------- | -------
400 | Bad Request -- Your request sucks
401 | Unauthorized -- Your authentication token is wrong
404 | Not Found -- The specified theme could not be found
405 | Method Not Allowed -- You tried to access a theme with an invalid method
410 | Gone -- The theme requested has been removed from our servers
418 | I'm a teapot
500 | Internal Server Error -- We had a problem with our server. Try again later.
503 | Service Unavailable -- We're temporarially offline for maintanance. Please try again later.
