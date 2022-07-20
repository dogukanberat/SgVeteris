# SgVeterisPostman

_https://www.getpostman.com/collections/0a8518c4dff0341b2c23_

## API Test Scenarios

---
- Merchant should be able to authorize and get token with login credentials

  _Expectation: Merchant should be received correct token code_


```http
  POST /auth/token
```
**REQUEST OBJECT**

| Parameter        | Value         | 
|:----------------|:--------------|
| `merchant_code` | `20720085303` | 
| `password`      | `f3bf10e5-ce97-4364-bf9e-1606bf450465`       |

`Send post request with this parameters and get response token and set next requests header
`

**_RESPONSE_**

`{
"code": "00",
"message": "APPROVED",
"data": {
"token": "eyJhbGciOiJSUzI1NiIsInR5cCIgOiAiSldUIiwia2lkIiA6ICJoOER5QjYxdTFvTy1lSERSZ0lYMTUwY3l1YzNSWmFTbDNlS0RQWjY3c1BzIn0.eyJqdGkiOiJjYTZkZmVhMS0yM2ZlLTQwYmEtYTBiNC03OWFkMDJjZjM1OWUiLCJleHAiOjE2NTgzNzU1MTYsIm5iZiI6MCwiaWF0IjoxNjU4MzM5NTE2LCJpc3MiOiJodHRwczovL2F1dGgtc2FuZGJveC5iaXRwYWNlLmNvbS9hdXRoL3JlYWxtcy9iaXRwYWNlIiwic3ViIjoiODI2NWI1YmQtODIxNy00YWQxLWJhNWMtZGYwNGE2MTQzYzY3IiwidHlwIjoiQmVhcmVyIiwiYXpwIjoibWVyY2hhbnQtYXBpIiwiYXV0aF90aW1lIjowLCJzZXNzaW9uX3N0YXRlIjoiYjZiYTRiM2QtMGFlMC00ZDUzLWIzN2UtZTA1NGEwY2NmMTcwIiwiYWNyIjoiMSIsInNjb3BlIjoicHJvZmlsZSBlbWFpbCIsImVtYWlsX3ZlcmlmaWVkIjp0cnVlLCJyb2xlcyI6WyJXSVRIRFJBVyIsIlBBWU1FTlQiLCJTRUxMIiwiQlVZIiwiREVQT1NJVCJdLCJwcmVmZXJyZWRfdXNlcm5hbWUiOiIyMDcyMDA4NTMwMyIsIm1lcmNoYW50X2lkIjoiNDM5In0.o-L2k4PFtWqbgZwcg7t3zW4q35dI35S8Mdneookg6FKhnJMc83fKgwqtItbw3fzeodzVRhsC42FAbJeSwyOsY3YIwqiSd-UL0iPReoNAmz4jjImr324YVRFh3ZBIrSLMTNwtKBEJmz2iN6pg5wg8Rpmaocm6KjYpxCc2Ce1Xd2LtPlzYQRwtDlZoDZ661Zt0u36yIC4fgMvTJRc_8uTWTdEGgA6WDJYujwlyG34e4OjEos3UIZtkX0X2q3qDdxMAL1j0XM-J7GL7fJhV75xm7RzsNG_WXrqEBlm18nuC3yhw9-YB9pLMwcQhfNo-iXxUytOumq3D-hA62gOof7MtFA"
},
"status": "APPROVED"
}`

---
- Merchant tries to login with invalid credentials

  _Expectation: Merchant should be received an error message_

```http
  POST /auth/token
```
**REQUEST OBJECT**

| Parameter        | Value         | 
|:----------------|:--------------|
| `merchant_code` | `20720085303` | 
| `password`      | `test1`       |

`Send post request with this wrong parameters
`

**_RESPONSE_**

`{
"code": "401",
"message": "Unauthorized access",
"status": "DECLINED",
"traceId": "0c942e22497b55b8"
}
`

---
- Merchants can receive BTC buy rate using correct token

  _Expectation: Merchant should be received the rate._

```http
  GET /buy/prices/BTC
```
`Send GET request to api /buy/prices/BTC with Auth Token
`


**_RESPONSE_**

`{
"code": "00",
"message": "Response Approved",
"data": {
"currency": "EUR",
"cryptocurrency": "BTC",
"buy_price": 23813.0183
},
"status": "APPROVED",
"traceId": "fbf92d46c4893ec2"
}`



---
- Merchant calls incorrect cryptocurrency code "etc" using correct token
  _Expectation: Merchant should be received an unsupported cryptocurrency message_


```http
  GET /buy/prices/etc
```
`  Send GET request to api /buy/prices/etc with Auth Token
`

**_RESPONSE_**

`{
"code": "150",
"message": "Unsupported cryptocurrency",
"status": "DECLINED",
"traceId": "3b3a01cf3da592a3"
}`

---
- Merchant can create a btc address using Create Deposit Address endpoint.
  _Expectation: Merchant should be received a BTC address_


```http
  POST /customer/deposit/address
```
**REQUEST OBJECT**

| Parameter        | Value            | 
|:----------------|:-----------------|
| `cryptocurrency` | `btc`            | 
| `customer`      | `CUSTOMEROBJECT` |

**CUSTOMER OBJECT**

| Parameter        | Value            | 
|:----------------|:-----------------|
| `reference_id` | `20720085303`            | 
| `first_name`      | `Dogukan` |
| `last_name`      | `Elbasan` |
| `email`      | `dogukanelbasan0@gmail.com` |
`  Send post request to api /customer/deposit/address with Auth and Correct Data`

**_RESPONSE_**

`{
"code": "00",
"message": "Response Approved",
"data": {
"code": "BTC",
"address": "2My4rq8ANgGCVSSDZ9YkxRcbGUkPbKPGccg"
},
"status": "APPROVED",
"traceId": "836876cb5d80897d"
}`
---