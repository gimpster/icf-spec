
## Error Handling:
Any response with an HTTP status code other outside the 2xx range indicates something is wrong and the response will be an error object.
The implementer is expected to detect and handle errors appropriately.

### Example Error Object
```javascript
[{
	"errorCode": 9000,
	"errorMessage": "A generic error has occured. Please review your request before trying again.",
	"fieldName": null
},
{
	"errorCode": 9001,
	"errorMessage": "The `supplierId` provided is missing or invalid.",
	"fieldName": "supplierId"
}]
```
**Fields:**
* `errorCode` contains a numeric error code
* `errorMessage` contains a human readable error message.
* `fieldName` can be either a string or null

The error response is an array of objects.
Although interrupting request execution when encountering the first error is valid, it is preferred that a list of multiple errors is returned (if applicable).
This enables the consumer to appropriately handle each error in independently, such as raising an alarm.


## Error Codes:
### HTTP level (Global):
- HTTP 400: Invalid request such as missing required query parameters, invalid request model, missing `Timestamp` header that is used to generate HMAC key, etc.
- HTTP 401: Missing `Authentication` header with HMAC key or key could not be validated
- HTTP 403: The `Authentication` header was validated but requester does not have correct permissions
- HTTP 404: Invalid URL path
- HTTP 500: It's unclear what went wrong, but the server can't respond in a sensible way. There may not even be an error object in the response body.


### Errors
**Generic errors**
- `ErrorCode` 9000: Could not parse request.
- `ErrorCode` 9001: A field in the request body is missing or invalid. (`errorMessage` should indicate which one is invalid)

**Specific errors**
- `ErrorCode` 9010: The provided `supplierId` url parameter is missing or invalid
- `ErrorCode` 9011: The provided `productId` url parameter is missing or invalid
- `ErrorCode` 9012: The provided `localDateStart` url parameter is missing or invalid
- `ErrorCode` 9013: The provided `localDateStart` url parameter is in the past
- `ErrorCode` 9014: The provided `localDateEnd` url parameter is missing or invalid
- `ErrorCode` 9015: The provided `localDateEnd` url parameter is in the past
- `ErrorCode` 9016: The provided `optionId` url parameter is missing or invalid
- `ErrorCode` 9017: The provided `uuid` url parameter is invalid


### Other guidelines
- An error during a "create" action such as placing a booking should be a guarantee that the booking was not finalized and shall not be charged. **One for the SLA maybe?**

**Motivation**
> There could be many different errors which could be caused by an invalid request. Those are generally easier to handle in a prescribed way.
> Errors that happen in the software that embeds the ICF specification are not easy to standardize.
> Therefor a quite generic set of errors has been specified that enable the consumer to explicitly monitor for more serious situations such as mapping problems.
> An exhaustive list of all possible request object fields that could be missing or invalid has been skipped, but _may_ be added in the future.
> 
> There is no need to distinguish endpoints in the error codes because the  URL you called when encountering the failure tells you that. 
