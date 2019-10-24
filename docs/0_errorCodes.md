## Error Codes:

### Global:
- HTTP 400: Invalid request such as missing `Timestamp` header that is used to generate HMAC key, missing required query parameters, invalid request model, etc.
	- `ErrorCode` 9000: Unable to process request. General catch-all for errors that do not fit into a more specific `ErrorCode`.
- HTTP 401: Missing `Authentication` header with HMAC key or key could not be validated
- HTTP 403: The `Authentication` header was validated but requestor does not have correct permissions
- HTTP 404: Invalid URL path

### Supplier List:
- None

### Product List:
- HTTP 400
	- ErrorCode 9011: The `supplierId` requested is invalid or has not shared products with the Reseller

### Availability Overview:
- HTTP 400:
	- `ErrorCode` 9021: The `supplierId` provided is invalid
	- `ErrorCode` 9022: The `productId` provided is invalid
	- `ErrorCode` 9025: The `localDateStart` provided is invalid or occurs in the past
	- `ErrorCode` 9025: The `localDateEnd` provided is invalid of occurs in the past

### Availability Check
- HTTP 400:
	- `ErrorCode` 9021: The `supplierId` provided is invalid
	- `ErrorCode` 9022: The `productId` provided is invalid
	- `ErrorCode` 9023: The `optionId` provided is invalid
	- `ErrorCode` 9025: One or more of the `availabilityIds` provided are invalid (`ErrorMessage` should indicate which one is invalid)
	- `ErrorCode` 9026: One or more of the `units.id` provided are invalid (`ErrorMessage` should indicate which one is invalid)
	- `ErrorCode` 9027: `quantity` requested for a `units.id` exceeds available quantity. (`ErrorMessage` should indicate which Unit `id` exceeds available quantity)
	- `ErrorCode` 9028: `quantity` requested for a `units.id` does not meet the minimum required for booking. (`ErrorMessage` should indicate which Unit `id` does not meet the minimum and what the minimum is)

### Create Reservation
- HTTP 400:
	- `ErrorCode` 9031: The `supplierId` provided is invalid
	- `ErrorCode` 9032: The `productId` provided is invalid
	- `ErrorCode` 9033: The `optionId` provided is invalid
	- `ErrorCode` 9034: The `uuid` provided is invalid
	- `ErrorCode` 9035: The `unitItems` provided is invalid
	- `ErrorCode` 9036: One or more of the `unitItems.unitId` is invalid (`ErrorMessage` should indicate which one is invalid)

### Extend Reservation
- HTTP 400:
	- `ErrorCode` 9041: The `supplierId` provided is invalid
	- `ErrorCode` 9044: The `uuid` provided cannot be found
	- `ErrorCode` 9045: The `reason` provided is invalid

### Expire Reservation
- HTTP 400:
	- `ErrorCode` 9051: The `supplierId` provided is invalid
	- `ErrorCode` 9054: The `uuid` provided is invalid

### Confirm Reservation
- HTTP 400:
	- `ErrorCode` 9061: The `supplierId` provided is invalid
	- `ErrorCode` 9064: The `uuid` provided is invalid

### Create Cancellation Request
- HTTP 400:
	- `ErrorCode` 9071: The `supplierId` provided is invalid
	- `ErrorCode` 9074: The `bookingUuid` provided is invalid
	- `ErrorCode` 9075: The `reason` provided is invalid

### Expire Cancellation Request
- HTTP 400:
	- `ErrorCode` 9081: The `supplierId` provided is invalid
	- `ErrorCode` 9084: The `uuid` provided is invalid

### Confirm Cancellation Request
- HTTP 400:
	- `ErrorCode` 9091: The `supplierId` provided is invalid
	- `ErrorCode` 9094: The `bookingUuid` provided is invalid
	- `ErrorCode` 9095: The `reason` provided is invalid

### Get Booking
- HTTP 400:
	- `ErrorCode` 9101: The `supplierId` provided is invalid
	- `ErrorCode` 9104: The `uuid` provided is invalid