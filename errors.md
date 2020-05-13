# Errors

## Webhook code

This is the error code returned in webhook after successfully calling the API.

| Code | Error | Description |
|---|---|---|
| 101 | WRONG_CREDENTIALS | Username or password is not correct for this merchant. |
| 102 | WRONG_CAPTCHA | Solve captcha failed 3-5 times. |
| 103 | ACCOUNT_IN_USE | Account is already loged in and need to wait 10 minutes before login again. |
| 104 | NO_ACCOUNT_FOUND | The result has no detectable account. |
| 105 | INVALID_CREDENTIALS | Invalid username / email. |
| 106 | CREDENTIAL_MAX_ATTEMPTS_EXCEEDED | Account can not be login due to continuous failed attempt. |
| 107 | ACCOUNT_LOCKED | Account has been lock and can not be login in. |
| 108 | PASSWORD_EXPIRED | Merchant require user to change password before going to next page. |
| 109 | ACCOUNT_NOT_SUPPORT | This account is currently not support by our API. |
| 110 | NOT_COMPANY_ACCOUNT | The credential is for personal account but trying to login in business portal. |
| 111 | IS_COMPANY_ACCOUNT | The credential is for business account but trying to login in personal portal. |

| Code | Error | Description |
|---|---|---|
| 201 | TIMED_OUT | The request took over 5 minutes to complete. |
| 202 | REQUEST_MAX_ATTEMPTS_REACHED | The request failed and can not be retry. |
| 203 | PROGRESS_PAGE_ABORTED | Deprecated in newest Api. User close the browser when login. |
| 204 | INVALID_JOB | The request is invalid. |
| 205 | DUPLICATED_JOB | Two or more request with the same id. |

| Code | Error | Description |
|---|---|---|
| 301 | NETWORK_FAILED | Network problem between Finsify and merchant. |
| 303 | PROCESS_CRASHED | Finsify process crashed. |
| 304 | MERCHANT_ERROR | Could not get data for some reason, mostly Finsify fault. |
| 305 | MERCHANT_TIMEOUT | Merchant throw timeout error. |
| 306 | LOAD_MERCHANT_FAILED | Merchant had been disable but still being called. |
| 307 | MERCHANT_UNDER_MAINTENANCE | Merchant website is under maintanance. |
| 308 | PROCESS_KILLED_BY_FINSIFY | This job killed by Finsify. |
| 309 | UNABLE_TO_OPEN_PAGE | Merchant website could not be opened. |
| 311 | PAGE_LOAD_SLOWER | Merchant website took too long to load. |
| 314 | BROWSER_LAUNCH_FAILED | Finsify could not open browser for this merchant. |

| Code | Error | Description |
|---|---|---|
| 401 | DATA_ERROR | Data sent through API is invalid. |
| 501 | JSON_PARSE_FAILED | Data sent through API could not be parsed. |
| 502 | INVALID_DATA | Data received from crawler is invalid. |
| 503 | DECRYPT_FAILED | Encrypted data could not be decrypt. |
| 601 | CATEGORIZE_FAILED | Auto categorize failed. |
| 602 | CAPTCHA_FAILED | Auto captcha solver failed. |
| 999 | UNKNOWN_ERROR | Unknown error. |
| 1000 | INVALID_TRANSFER_INFO | Invalid money transfer request. |
| 1001 | WRONG_OTP | Wrong OTP submited. |
| 1100 | WEBHOOK_ERROR | Could not sent webhook to partner. |

## HTTP status code

The Finsify API uses the following error codes in HTTP status. This is mostly deprecated in the newest version of our API.

| Code | Error | Description |
|---|---|---|
| 400 | BadRequest | Invalid Request |
| 404 | AccountNotFound | Account is not found - Your account request not found in server |
| 404 | ClientNotFound | Can't find client with your id |
| 503 | ConnectError | We're temporarily offline. Please try again later. |
| 400 | ContentInputInvalid | Only allow data type application/json |
| 400 | CredentialInvalid | Credentials is invalid |
| 500 | CustomerCreateError | Can't create new customer. Please try later. |
| 400 | CustomerExists | Your customer is exists |
| 404 | CustomerNotFound | Can't find your customer. |
| 400 | DataInvalid | Data is invalid |
| 500 | InternalError | Sorry server is crash. Please try again. |
| 404 | LoginNotFound | Login is not found - Can't find your login in server |
| 503 | ServerMaintenance | Servers are currently undergoing maintenance. Please try later |
| 404 | ServiceNotFound | Service is not found - Your service request is not define |
| 500 | TokenCreateError | Can't create a token. Please try again. |
| 400 | TokenExpire | Your token is expired. Please create new token. |
