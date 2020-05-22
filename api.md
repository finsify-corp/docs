# API

## Api Base

|  |  |
|---|---|
| Schema | https |
| DEV Host | https://trial-api.finsify.com |
| Production Host | COMING SOON |
| HTTPS protocol support | TLSv1.2, TLSv1.3 |
| Postman sample | https://www.getpostman.com/collections/4d7f6e8ff52a5e7106bb |

## Request Crawler

### Method

|  |  |
|---|---|
| Base path	| /api/request |
| HTTP method | POST |
| Content-Type | application/json |
| Encryption KEY | RSA Public Key provide by Finsify |

### Request

#### Header

| Parameters | Type | Description | Required |
|---|---|---|---|
| encrypted	| string | ON DEV SERVER ONLY. Set value is “1” for enable encrypted. | Yes |
| x-client-id | string | Provided by Finsify. | Yes |
| Content-Type | string | Unique code to identify your customer. | Yes |

#### Body

| Parameters | Type | Description |
|---|---|---|
| data	| string | AES CTR 256 bit encrypted data in hex, structure as json with information below. |
| key | string | AES decryption key encrypted by RSA public key. Key must be random generated for every request. Key is in JSON format like [82, 22, 180, 226, 160, 167, 221, 201, …] |

#### Data

| Parameters | Type | Description | Required |
|---|---|---|---|
| credential | string/json | User credential sample: {"username":"moneylover", "password":"asdasdasd"} | Yes |
| service_id | int | Service ID provided by Finsify. Read more [List of service](service.md) | Yes |
| callback_url | string | Url for your webhook | Yes |
| type | string | `manual` or `auto`. Manual for first time link and auto for getting transaction for linked account. Default is auto. Web hook will be sent In manual mode for every step, in auto mode only when completed. | Optional |
| only_get_accounts | bool | Default is `false`. If `true` then it will only return list of accounts with empty array for transaction [ ] and no callback for transaction list. | Optional |
| filter_accounts | Arrray[string] | Id of the accounts user have already chosen to link (for user already use the service and want to get new transactions, also don’t use only_get_accounts at the same time with filter_accounts) | Optional |

- First time user should be: `type`: `manual` and `only_get_accounts`: `true`. 
- Return user should be: `type`: `auto`, `only_get_accounts`: `false`, `filter_accounts`: [`sample-account-id`]

Sample data:

```javascript
{
    “credential”:”xxxxxxxxxxxxxxxxxx”,
    “customer_id”:”abcd-efgh-ijkl-mnop”,
    “service_id”:20,
    “callback_url”:”https://api.moneylover.me/finsify/calback”,
    “filter_accounts”: [“vcb-vn-001104080916”]
}
```

Sample unencrypted data request:

```bash
curl -X POST 'https://trial-api.finsify.com/api/request' \
--header 'Content-Type: application/json' \
--header 'x-customer-id: 121321312' \
--header 'X-CLIENT-ID: f43568ab' \
--header 'Content-Type: application/json' \
--header 'encrypted: 0' \
--data-raw '{
    "data": {
        "credentials": {
            "username": "xxxxxxxx",
            "password": "xxxxxxxx"
        },
        "service_id": 249,
        "callback_url": "https://en0owazxol4fum.x.pipedream.net",
        "only_get_accounts": false,
        "type": "auto"
    }
}'
```

Sample encrypted data request:

```bash
curl -X POST 'https://trial-api.finsify.com/api/request' \
--header 'Content-Type: application/json' \
--header 'x-customer-id: 121321312' \
--header 'X-CLIENT-ID: f43568ab' \
--header 'Content-Type: application/json' \
--header 'encrypted: 1' \
--data-raw '{
"data": "0f0990a27e153b5fd26581d3f317e4c35e8a741138fb3c0633f818f1eb8f299c9bcb019351da22fae0d5f06178f144477951a14f2c14ed4aa2f7ba1ca689dfb040b04e755bf51426a0e93403a084379af692c602f7889dj84n3uedf917d2e87f3bd887a80eba4f79f92f9b014b7fe07b2ce88c6bdd43047f86bd0d02d45aff9382700f6846b96a2cb3adf84e2d6a4e168ec7cc012672600b1f910e8ba0029ad4922eb1b01048f313c87c2be184635ae309481",
"key": "L5NqVfGdwAD10jvXUIqRDf3X8gMDTAENABDzWxj4NSXCeEURWc53HHzqylmvvExdvvYX0aFVa38IH4vk1qbQT3Cuv9HFPC477WTrrj+o9+2+Qn5TbS1WpNzboHwOl3wz1x9Om4TH78hwNkY8dH5LYyKe4GpEc8zsDYhF8+rOZe+GQjX8lWhZJ4pr+bkuc0nLvEyAwCfU3pEQuIIRfFdgvMGnnXr5+4XSntTBDQ60k/ctkIwSpvsZ1fcwdSG70PmcK6vX+Iq+ZEPkKVjR2hBshX21f0jGZ3Yxnu343cgnqFiHIEHbZiPD+cuNUe5PmDWcIcz8IT+ccyExSfBsl1dNPQ=="
}'
```

### Response

#### Successful

|  |  |
|---|---|
| Status code | 202 (Accepted) |
| Body	| json |

```javascript
{“request_id”: “398e08b5-44c0-4590-ae13-2fd50cd54824”}
```

#### Failure

|  |  |
|---|---|
| Status code | 400 |

```javascript
{
“request_id”: “398e08b5-44c0-4590-ae13-2fd50cd54824”,
“error”: ”a message error”
}
```

## Webhook

#### Event states of the crawler

| State | Description |
|---|---|
| request.ready | Crawler is starting with the request_id. |
| request.failed | Not successful getting data, "error" will be return below. |
| request.successful | Successful getting data, "data" will be return below, this is the final webhook on the request_id. |
| merchant.progress | State of the crawler changed, see "progress" for more info. Tasks may include:<br /> - login, account<br /> - filter-account<br /> - skip-transaction-task<br /> - transaction. |
| merchant.successful | All the task above is completed. |

## Cancel Request

Cancel in running request.

Sent DELETE request to: /api/request/{request_id}

```bash
curl -X DELETE \
  https://trial-api.finsify.com/api/request/f19a5292-7e6a-4c87-8185-984686a6c0bd \
  -H 'Content-Type: application/json' \
  -H 'cache-control: no-cache'
```

## Sent OTP, secret password

### Method

|  |  |
|---|---|
| Base path	| /api/request/{requestID}/otp |
| HTTP method | PUT |
| Content-Type | application/json |

### Body

Encrypted using the same method as above. sample unencrypt data:

```
{
 "otp": "1234"
}
```

### Sample

Sample unencrypted on test server:

```bash
curl --location --request PUT 'https://trial-api.finsify.com/api/request/9763e0c1-250b-4542-93d3-7d61987551c0/otp' \
--header 'X-CLIENT-ID: f43568ab' \
--header 'x-customer-id: 001' \
--header 'encrypted: 0' \
--header 'Content-Type: application/json' \
--data-raw '{"data": {
 "otp": "1234"
}}'
```

Sample encrypted data request:

```bash
curl --location --request PUT 'https://trial-api.finsify.com/api/request/9763e0c1-250b-4542-93d3-7d61987551c0/otp' \
--header 'X-CLIENT-ID: f43568ab' \
--header 'x-customer-id: 001' \
--header 'encrypted: 0' \
--header 'Content-Type: application/json' \
--header 'encrypted: 1' \
--data-raw '{
"data": "0f0990a27e153b5fd26581d3f317e4c35e8a741138fb3c0633f818f1eb8f299c9bcb019351da22fae0d5f06178f144477951a14f2c14ed4aa2f7ba1ca689dfb040b04e755bf51426a0e93403a084379af692c602f7889bd3345345345",
"key": "L5NqVfGdwAD10jvXUIqRDf3X8gMDTAENABDzWxj4NSXCeEURWc53HHzqylmvvExdvvYX0aFVa38IH4vk1qbQT3Cuv9HFPC477WTrrj+o9+2+Qn5TbS1WpNzboHwOl3wz1x9Om4TH78hwNkY8dH5LYyKe4GpEc8zsDYhF8+rOZe+GQjX8lWhZJ4pr+bkuc0nLvEyAwCfU3pEQuIIRfFdgvMGnnXr5+4XSntTBDQ60k/ctkIwSpvsZ1fcwdSG70PmcK6vX+Iq+ZEPkKVjR2hBshX21f0jGZ3Yxnu343cgnqFiHIEHbZiPD+cuNUe5PmDWcIcz8IT+ccyExSfBsl1dNPQ=="
}'
```
