/accounts
=========

* [Overview](#overview)
* [Account](#account)
* [GET /accounts](#retrieve-all-accounts)
* [GET /accounts/:id](#retrieve-account)
* [Issues](#issues)
* [Authors](#authors)

### Overview
Accounts API allows you to list / view all the accounts of the logged in customer. This includes energy accounts, services accounts, multi premise landlord accounts and sales orders of OAM registered and wafer thin profile customers. Responses from this API will be retuned in JSON format only.

### Account
Account as a resource represents following information

| Property | Type | Description |
| :-------------------- | :---------- | ------------------------------------------------------------ |
| id | string | `Returned always`. Account number or Sales Order number of the account is considered as the unique identifier |
| holderName | string | `Returned always`. Name of the account holder if available. |
| multiPremiseLandlord | boolean | `Returned always`. `true` if the account holder is a multi premise landlord, `false` otherwise. |
| status | string | `Returned always`. Status of the account if available. Possible values are `open`, `pending`, `closed`, `submitted`, `cancelled`, `complete`, `incomplete`, `locked`, `deactive`, `inprogress`, `new`, `processed`, `wafer` and `unknown`.|
| type | string | `Returned always`. Type of the account, this will be Energy, Services or Order. |
| subType | string | `Returned always`. Subtype of the account, this will be Electricity, Gas or Dual for Energy accounts and Sales orders, Home Services or Security for Services account. |
| responsibilityType | string | `Returned always`. Responsibility type of the account if available. Possible values are `Legal Payer`, `Contract Owner` and `Other Contract Owner`. | 
| supplyAddress | Address | `Returned always`. Address of the customer if available. MPAN and MPRN is null, as these values are not available for the address in backend. |

### Retrieve all accounts
```
GET /accounts
Authorization: Bearer accesstoken
cid: clientid
```
#### Parameters
No parameters required for fetching the accounts resource.

#### Response

```
Status: 200 OK
Content-Type: application/json
```
```json
{
    "status": "SUCCESS",
    "data": {
        "accounts": [
            {
                "id": "850034235409",
                "multiPremiseLandlord": false,
                "status": "open",
                "subType": "Electricity",
                "responsibilityType": "Legal Payer",
                "supplyAddress": {
                    "MPRN": null,
                    "postalTown": "Salford",
                    "houseName": "",
                    "address": "53b, Garstang Road North, Salford, Lancashire, WS3 3ER",
                    "county": "LANCASHIRE",
                    "MPAN": null,
                    "houseNumber": "53B",
                    "postcode": "WS3 3ER",
                    "addressLine2": "",
                    "addressLine1": "GARSTANG ROAD NORTH",
                    "flatNumber": null
                },
                "type": "Energy",
                "holderName": "Mr Morita"
            },
            {
                "id": "850034336151",
                "multiPremiseLandlord": false,
                "status": "open",
                "subType": "Gas",
                "responsibilityType": "Legal Payer",
                "supplyAddress": {
                    "MPRN": null,
                    "postalTown": "Salford",
                    "houseName": "",
                    "address": "53b, Garstang Road North, Salford, Lancashire, WS3 3ER",
                    "county": "LANCASHIRE",
                    "MPAN": null,
                    "houseNumber": "53B",
                    "postcode": "WS3 3ER",
                    "addressLine2": "",
                    "addressLine1": "GARSTANG ROAD NORTH",
                    "flatNumber": null
                },
                "type": "Energy",
                "holderName": "Mr Morita"
            }
        ]
    },
    "errors": [],
    "meta": {}
}
```
#### Possible Errors
##### Case 1: Customer is not authenticated
When you request without a valid access token in Authorization Request Header, API responses with following

```
Status: 401 Authorization Required 
Content-Type: application/json
```
```json
{
    "status": "FAIL",
    "data": {},
    "errors": {
        "authorize": "access_denied"
    },
    "meta": {}
}
```
### Retrieve account
```
GET /accounts/:accountNumber
Authorization: Bearer accesstoken
cid: clientid
```
#### Parameters
No parameters required for fetching the accounts resource.

#### Response

```
Status: 200 OK
Content-Type: application/json
```
```json
{
    "status": "SUCCESS",
    "data": {
        "account": {
            "id": "850034235409",
            "multiPremiseLandlord": false,
            "status": "open",
            "subType": "Electricity",
            "responsibilityType": "Legal Payer",
            "supplyAddress": {
                "MPRN": null,
                "postalTown": "Salford",
                "houseName": "",
                "address": "53b, Garstang Road North, Salford, Lancashire, WS3 3ER",
                "county": "LANCASHIRE",
                "MPAN": null,
                "houseNumber": "53B",
                "postcode": "WS3 3ER",
                "addressLine2": "",
                "addressLine1": "GARSTANG ROAD NORTH",
                "flatNumber": null
            },
            "type": "Energy",
            "holderName": "Mr Morita"
        }
    },
    "errors": [],
    "meta": {}
}
```
#### Possible Errors
##### Case 1: Customer is not authenticated
When you request without a valid access token in Authorization Request Header, API responses with following

```
Status: 401 Authorization Required 
Content-Type: application/json
```
```json
{
    "status": "FAIL",
    "data": {},
    "errors": {
        "authorize": "access_denied"
    },
    "meta": {}
}
```
##### Case 2: Account is not available for the customer
When you request an accountNumber which is not part of the customer, API responses with following

```
Status: 404 Not Found 
Content-Type: application/json
```
```json
{
    "status": "ERROR",
    "data": {},
    "errors": {
        "accountNumber": "error.client.account.notfound"
    },
    "meta": {}
}
```

### Issues
* No known issues at this moment

### Authors
@haneesa, @gpradeepkrishna, @junaid, @sakthi
