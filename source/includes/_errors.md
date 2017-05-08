# Errors

The Amplo API uses the following error codes:

Error Code | Meaning
---------- | -------
400 | Bad Request -- The parameters of your request were incorrect or malformed
401 | Unauthorized -- Incorrect API Key provided
403 | Forbidden -- The API Key is correct, but the request is for something the Key does not have permission to view.
404 | Not Found -- The specified object could not be found
405 | Method Not Allowed -- The action requested could not be performed
406 | Not Acceptable -- The request was not correctly formatted JSON
410 | Gone -- The object requested has been removed from our servers
429 | Too Many Requests -- Rate limit exceeded.  
500 | Internal Server Error -- An error occurred on our servers.  Please wait and try again later, or contact support.
503 | Service Unavailable -- We're temporarily offline for maintenance. Please try again later.
