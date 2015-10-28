## Group Accounts
Accounts API allows you to list / view all the accounts of the logged in customer. This includes energy accounts, services accounts, multi premise landlord accounts and sales orders of OAM registered and wafer thin profile customers. Responses from this API will be retuned in JSON format only.

## Accounts Collection [/accounts]
### Retrieve a specific Account [GET /accounts/{accountNumber}]
+ Parameters

    + accountNumber (number) ...This is the customers account number

+ Request

    + Headers

            Authorization: Bearer accesstoken
            cid: 05e230bf-a9cf-4b31-bc54-d3a995f62526

+ Response 200 (application/json)

        {
            "status": "SUCCESS",
            "data": {
                "account": {
                    "id": "850034235409",
                    "multiPremiseLandlord": false,
                    "status": "Open",
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

+ Response 401 (application/json)

        {
            "status": "FAIL",
            "data": {},
            "errors": {
                "authorize": "access_denied"
            },
            "meta": {}
        }

+ Response 404 (application/json)

        {
            "status": "ERROR",
            "data": {},
            "errors": {
                "accountNumber": "error.client.account.notfound"
            },
            "meta": {}
        }

### Retrieve all Accounts [GET /accounts]
+ Request

    + Headers

            Authorization: Bearer accesstoken
            cid: 05e230bf-a9cf-4b31-bc54-d3a995f62526

+ Response 200 (application/json)

        {
            "status": "SUCCESS",
            "data": {
                "accounts": [
                    {
                        "id": "850034235409",
                        "multiPremiseLandlord": false,
                        "status": "Open",
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
                        "status": "Open",
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

+ Response 401 (application/json)

        {
            "status": "FAIL",
            "data": {},
            "errors": {
                "authorize": "access_denied"
            },
            "meta": {}
        }
## Energy Accounts [/energy-accounts]
Energy Accounts API allows you to list / view all the energy accounts of the logged in customer. Responses from this API will be retuned in JSON format only
Energy Account as a resource represents following information

+ id - (string) - Account number of the account is considered as the unique identifier
+ holderName - (string) - Name of the account holder if available
+ status - (string) - Status of the account if available. Possible values are open, pending, closed, submitted, cancelled, complete, incomplete, locked, deactive, inprogress, new, processed, wafer and unknown
+ type - (string) - Type of the account, this will be always Energy.
+ subType - (string) - Subtype of the account, this will be Electricity, Gas or Dual
+ responsibilityType - (string) - Responsibility type of the account if available.
+ balance - (string)  - Balance of the account if available.
+ balanceType - (string) - Type of account balance if available, it can be either "in credit" or "in debit".
+ tariff - (string) -  Tariff id associated to the account if available.
+ paymentType - (string) -  Payment type description of the account if available.
+ contractEndDate - (string) - End date of contract associated to the account if available, in dd/MM/yyyy format 
+ supplyAddress - (Address) -  Address of the customer if available. MPAN and MPRN is null, as these values are not available for the address in backend.
+ jointInvoiceDetails - (object) -  Holds details of the merge related information only if the account was merged previously. 
+ registeredPaperlessBillingOn - (string) - Represents the date when Paperless billing was opted in for this account. 
+ paperlessBilling - (boolean) - true if account is opted into paperless billing, false otherwise. 
+ jointInvoiced - (boolean) - true if the account is a Joint Invoiced account. false otherwise.

### Retrieve all energy accounts [GET /energy-accounts]
+ Request

    + Headers

            Authorization: Bearer accesstoken
            cid: 05e230bf-a9cf-4b31-bc54-d3a995f62526
            
+ Response 200 (application/json)

        {
            "status": "SUCCESS",
            "data": {
                "energyAccounts": [
                    {
                        "jointInvoiceDetails": {
                            "mergeDate": null,
                            "mergeType": null,
                            "mergedAccountNumber": null
                        },
                        "registeredPaperlessBillingOn": "04/02/2011",
                        "status": "open",
                        "paymentType": "Direct Debit",
                        "responsibilityType": "Legal Payer",
                        "paperlessBilling": true,
                        "type": "Energy",
                        "holderName": "Mr Morita",
                        "id": "850034235409",
                        "contractEndDate": null,
                        "balance": 111.47,
                        "subType": "Electricity",
                        "tariff": "fix-and-fall-june-2016",
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
                        "balanceType": "in credit",
                        "jointInvoiced": true
                    },
                    {
                        "jointInvoiceDetails": {
                            "mergeDate": null,
                            "mergeType": null,
                            "mergedAccountNumber": null
                        },
                        "registeredPaperlessBillingOn": "04/02/2011",
                        "status": "open",
                        "paymentType": "Direct Debit",
                        "responsibilityType": "Legal Payer",
                        "paperlessBilling": true,
                        "type": "Energy",
                        "holderName": "Mr Morita",
                        "id": "850034336151",
                        "contractEndDate": null,
                        "balance": 140.52,
                        "subType": "Gas",
                        "tariff": "fix-and-fall-june-2016",
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
                        "balanceType": "in credit",
                        "jointInvoiced": true
                    }
                ]
            },
            "errors": [],
            "meta": {}
        }
        
+ Response 401 (application/json)

        {
            "status": "FAIL",
            "data": {},
            "errors": [
                {
                    "code": "authorize",
                    "message": "access_denied"
                }
            ],
            "meta": {}
        }


### Retrieve a specific Account [GET /energy-accounts{?accountNumber*}]
+ Parameters

    + accountNumber (number) ...This is the customers account number
        
+ Request

    + Headers

            Authorization: Bearer accesstoken
            cid: 05e230bf-a9cf-4b31-bc54-d3a995f62526

+ Response 200 (application/json)

        {
            "status": "SUCCESS",
            "data": {
                "energyAccounts": [
                    {
                        "jointInvoiceDetails": {
                            "mergeDate": null,
                            "mergeType": null,
                            "mergedAccountNumber": null
                        },
                        "registeredPaperlessBillingOn": "04/02/2011",
                        "status": "open",
                        "paymentType": "Direct Debit",
                        "responsibilityType": "Legal Payer",
                        "paperlessBilling": true,
                        "type": "Energy",
                        "holderName": "Mr Morita",
                        "id": "850034235409",
                        "contractEndDate": null,
                        "balance": 111.47,
                        "subType": "Electricity",
                        "tariff": "fix-and-fall-june-2016",
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
                        "balanceType": "in credit",
                        "jointInvoiced": true
                    },
                    {
                        "jointInvoiceDetails": {
                            "mergeDate": null,
                            "mergeType": null,
                            "mergedAccountNumber": null
                        },
                        "registeredPaperlessBillingOn": "04/02/2011",
                        "status": "open",
                        "paymentType": "Direct Debit",
                        "responsibilityType": "Legal Payer",
                        "paperlessBilling": true,
                        "type": "Energy",
                        "holderName": "Mr Morita",
                        "id": "850034336151",
                        "contractEndDate": null,
                        "balance": 140.52,
                        "subType": "Gas",
                        "tariff": "fix-and-fall-june-2016",
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
                        "balanceType": "in credit",
                        "jointInvoiced": true
                    }
                ]
            },
            "errors": [],
            "meta": {}
        }

+ Response 401 (application/json)

        {
            "status": "FAIL",
            "data": {},
            "errors": [
                {
                    "code": "authorize",
                    "message": "access_denied"
                }
            ],
            "meta": {}
        }
        
+ Response 404 (application/json)

        {
            "status": "FAIL",
            "data": {},
            "errors": [
                {
                    "code": "authorize",
                    "message": "access_denied"
                }
            ],
            "meta": {}
        }

### Modify Energy Account [PUT /energy-accounts/{accountNumber}]
+ Parameters

    + accountNumber (number) ...This is the customers account number
        
+ Request

    + Headers

            Authorization: Bearer accesstoken
            cid: 05e230bf-a9cf-4b31-bc54-d3a995f62526

+ Response 200 (application/json)

            {
                "energyAccount": {
                    "jointInvoiceDetails": {
                        "mergeDate": null,
                        "mergeType": null,
                        "mergedAccountNumber": null
                    },
                    "registeredPaperlessBillingOn": "04/02/2011",
                    "status": "open",
                    "paymentType": "Direct Debit",
                    "responsibilityType": "Legal Payer",
                    "paperlessBilling": true,
                    "type": "Energy",
                    "holderName": "Mr Morita",
                    "id": "850034235409",
                    "contractEndDate": null,
                    "balance": 111.47,
                    "subType": "Electricity",
                    "tariff": "fix-and-fall-june-2016",
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
                    "balanceType": "in credit",
                    "jointInvoiced": true
                },
                "meta": {
                    "orderPayload": "eXJrazFFaXlKcC9qTlI3NWVSTEZzWkl0YWdOS0pSRTdXR2VscEErOTYxTkx3WFFGZXUwWURhMmhvbW1SaEUvcXQxTUZjbEtLL0JKbAp2VVIvV3k0MFVGNzc4TVdjUmpGREtqeS9nMzZUT0JCQTJPR3E0V05HcGRZZThGSU5EREc2NktNcXBrNnJmWEpUYUgxT2Z5RmVPenVSCmFrUVNoUTdUcVE2WVRTT2hKbUZtNVZwSEtFYjAyTWNHUXpldTFsWmZhUjczZDVLSTFIWFBGUnJNZWpKR1RZY25FZFEwNlpjT1c2OEwKTkRvU3MzYndxRmtiS0F5YjVkQ0krNFhFdnpUaktwTzN1RzJjTU42Q2RubUdlTUlvMXc9PQ"
                }
            }
            
+ Response 401 (application/json)

        {
            "status": "FAIL",
            "data": {},
            "errors": [
                {
                    "code": "authorize",
                    "message": "access_denied"
                }
            ],
            "meta": {}
        }
        
+ Response 404 (application/json)

        {
            "status": "FAIL",
            "data": {},
            "errors": [
                {
                    "code": "orderPayload",
                    "message": "error.client.orderPayload.invalid"
                }
            ],
            "meta": {}
        }
        
        
### Retrieve a specific Account [GET /energy-accounts/{accountNumber}]
+ Parameters

    + accountNumber (number) ...This is the customers account number
        
+ Request

    + Headers

            Authorization: Bearer accesstoken
            cid: 05e230bf-a9cf-4b31-bc54-d3a995f62526

+ Response 200 (application/json)

        {
            "status": "SUCCESS",
            "data": {
                "energyAccount": {
                    "jointInvoiceDetails": {
                        "mergeDate": null,
                        "mergeType": null,
                        "mergedAccountNumber": null
                    },
                    "registeredPaperlessBillingOn": "04/02/2011",
                    "status": "open",
                    "paymentType": "Direct Debit",
                    "responsibilityType": "Legal Payer",
                    "paperlessBilling": true,
                    "type": "Energy",
                    "holderName": "Mr Morita",
                    "id": "850034235409",
                    "contractEndDate": null,
                    "balance": 111.47,
                    "subType": "Electricity",
                    "tariff": "fix-and-fall-june-2016",
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
                    "balanceType": "in credit",
                    "jointInvoiced": true
                }
            },
            "errors": [],
            "meta": {}
        }
        
### Retrieve all energy accounts [GET /energy-accounts]
+ Request

    + Headers

            Authorization: Bearer accesstoken
            cid: 05e230bf-a9cf-4b31-bc54-d3a995f62526
            
+ Response 200 (application/json)

        {
            "status": "SUCCESS",
            "data": {
                "energyAccounts": [
                    {
                        "jointInvoiceDetails": {
                            "mergeDate": null,
                            "mergeType": null,
                            "mergedAccountNumber": null
                        },
                        "registeredPaperlessBillingOn": "04/02/2011",
                        "status": "open",
                        "paymentType": "Direct Debit",
                        "responsibilityType": "Legal Payer",
                        "paperlessBilling": true,
                        "type": "Energy",
                        "holderName": "Mr Morita",
                        "id": "850034235409",
                        "contractEndDate": null,
                        "balance": 111.47,
                        "subType": "Electricity",
                        "tariff": "fix-and-fall-june-2016",
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
                        "balanceType": "in credit",
                        "jointInvoiced": true
                    },
                    {
                        "jointInvoiceDetails": {
                            "mergeDate": null,
                            "mergeType": null,
                            "mergedAccountNumber": null
                        },
                        "registeredPaperlessBillingOn": "04/02/2011",
                        "status": "open",
                        "paymentType": "Direct Debit",
                        "responsibilityType": "Legal Payer",
                        "paperlessBilling": true,
                        "type": "Energy",
                        "holderName": "Mr Morita",
                        "id": "850034336151",
                        "contractEndDate": null,
                        "balance": 140.52,
                        "subType": "Gas",
                        "tariff": "fix-and-fall-june-2016",
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
                        "balanceType": "in credit",
                        "jointInvoiced": true
                    }
                ]
            },
            "errors": [],
            "meta": {}
        }
        
+ Response 401 (application/json)

        {
            "status": "FAIL",
            "data": {},
            "errors": [
                {
                    "code": "authorize",
                    "message": "access_denied"
                }
            ],
            "meta": {}
        }


## Service Accounts [/service-accounts]
Service Accounts API allows you to list / view all the service accounts of the logged in customer. Responses from this API will be retuned in JSON format only.
Service Account as a resource represents following information

+ id - (string) - `Returned always`. Account number of the account is considered as the unique identifier
+ customerId - (string) - `Returned always`. This is the legacy customer identification applicable for certain accounts.
+ premiseId - (string) - `Returned always`. This is the legacy premise identification applicable for certain accounts.
+ holderName - (string) - `Returned always`. Name of the account holder if available.
+ status - (string) - `Returned always`. Status of the account if available. Possible values are `open`, `pending`, `closed`, `submitted`, `cancelled`, `complete`, `incomplete`, `locked`, `deactive`, `inprogress`, `new`, `processed`, `wafer` and `unknown`
+ type - (string) - `Returned always`. Type of the account, this will be always Services.
+ subType - (string) - `Returned always`. Subtype of the account, this will be Home Services or Security.
+ responsibilityType - (string) - `Returned always`. Responsibility type of the account if available.
+ legacyAccountNumber - (string) - `Returned always`. Legacy Account Number of the account if available.
+ contractEndDate - (string) - `Returned always`. End date of contract associated to the account if available, in dd/MM/yyyy format
+ nextServiceDate - (string) - `Returned always`. Next service visit date if available, in dd/MM/yyyy format
+ multiPremiseLandlord- (boolean) - `Returned always`. Indicates the account as a multi premise landlord account, if the value is true
+ bulkAccount - (boolean) - `Returned always`. Indicates the account as a bulk account, if the value is true
+ landlord - (boolean) - `Returned always`. Indicates the account as a landlord account, if the value is true
+ gasSafetyCertificateAvailable - (boolean) - `Returned always`. Indicates that the account holds a valid Gas Safety Certificate, if the value is true
+ eligibleForFirstVisit - (boolean) - `Returned always`. Indicates that first visit can be booked for this account, if the value is true
+ eligibleForInterimBreakdown - (boolean) - `Returned always`. Indicates that interim breakdown visit can be booked for this account, if the value is true
+ eligibleForAnnualServiceVisit - (boolean) - `Returned always`. Indicates that annual service visit can be booked for this account, if the value is true
+ eligibleForUpsell - (boolean) - `Returned always`. Indicates that the account can be upgraded, if the value is true
+ supplyAddress - (Address) - `Returned always`. Address of the customer if available. MPAN and MPRN is null, as these values are not available for the address in backend.

### Retrieve all service accounts [GET /service-accounts]
+ Request

    + Headers

            Authorization: Bearer accesstoken
            cid: 05e230bf-a9cf-4b31-bc54-d3a995f62526
            
+ Response 200 (application/json)

            {
                "status": "SUCCESS",
                "data": {
                    "serviceAccounts": [
                        {
                            "landlord": false,
                            "legacyAccountNumber": "22208170L277092",
                            "status": "open",
                            "eligibleForAnnualServiceVisit": true,
                            "eligibleForUpsell": true,
                            "responsibilityType": "Legal Payer",
                            "type": "Services",
                            "holderName": "Mr Thomas Red",
                            "id": "911000155091",
                            "contractEndDate": "10/12/2015",
                            "gasSafetyCertificateAvailable": false,
                            "bulkAccount": false,
                            "customerId": "22208170",
                            "multiPremiseLandlord": false,
                            "subType": "Home Services",
                            "supplyAddress": {
                                "MPRN": null,
                                "postalTown": "Lightwater",
                                "houseName": null,
                                "address": "20, Springfield, Lightwater, Surrey, GU18 5XP",
                                "county": "SURREY",
                                "MPAN": null,
                                "houseNumber": "20",
                                "postcode": "GU18 5XP",
                                "addressLine2": null,
                                "addressLine1": "Springfield",
                                "flatNumber": null
                            },
                            "premiseId": "L277092",
                            "eligibleForInterimBreakdown": true,
                            "eligibleForFirstVisit": true
                        }
                    ]
                },
                "errors": [],
                "meta": {}
            }
            
+ Response 401 (application/json)

            {
                "status": "FAIL",
                "data": {},
                "errors": {
                    "authorize": "invalid_request"
                },
                "meta": {}
            }

### Retrieve a specific service account [GET /service-accounts/{accountNumber}]
+ Parameters

    + accountNumber (number) ...This is the customers account number
        
+ Request

    + Headers

            Authorization: Bearer accesstoken
            cid: 05e230bf-a9cf-4b31-bc54-d3a995f62526

+ Response 200 (application/json)

            {
                "status": "SUCCESS",
                "data": {
                    "serviceAccount": {
                        "landlord": false,
                        "legacyAccountNumber": "22208170L277092",
                        "status": "open",
                        "eligibleForAnnualServiceVisit": true,
                        "eligibleForUpsell": true,
                        "responsibilityType": "Legal Payer",
                        "type": "Services",
                        "holderName": "Mr Thomas Red",
                        "id": "911000155091",
                        "contractEndDate": "10/12/2015",
                        "gasSafetyCertificateAvailable": false,
                        "bulkAccount": false,
                        "customerId": "22208170",
                        "multiPremiseLandlord": false,
                        "subType": "Home Services",
                        "supplyAddress": {
                            "MPRN": null,
                            "postalTown": "Lightwater",
                            "houseName": null,
                            "address": "20, Springfield, Lightwater, Surrey, GU18 5XP",
                            "county": "SURREY",
                            "MPAN": null,
                            "houseNumber": "20",
                            "postcode": "GU18 5XP",
                            "addressLine2": null,
                            "addressLine1": "Springfield",
                            "flatNumber": null
                        },
                        "premiseId": "L277092",
                        "eligibleForInterimBreakdown": true,
                        "eligibleForFirstVisit": true
                    }
                },
                "errors": [],
                "meta": {}
            }

+ Response 401 (application/json)

            {
                "status": "FAIL",
                "data": {},
                "errors": {
                    "authorize": "invalid_request"
                },
                "meta": {}
            }

+ Response 404 (application/json)

            {
                "status": "ERROR",
                "data": {},
                "errors": {
                    "accountNumber": "error.client.account.notfound"
                },
                "meta": {}
            }
