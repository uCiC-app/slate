# Errors

uCiC uses conventional HTTP response codes to indicate the success or failure of an API request. In general, codes in the 2xx range indicate success, codes in the 4xx range indicate an error that failed given the information provided (e.g., a required parameter was omitted, a charge failed, etc.), and codes in the 5xx range indicate an error with Stripe's servers (these are rare).

We will soon be adding a unified error response structure.

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
