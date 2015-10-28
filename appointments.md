
/appointments
=============

* [Overview](#overview)
* [Appointment](#appointment)
* [GET /appointments](#get-appointments)
* [GET /appointments?accountNumber=:accountNumber...](#get-appointmentsaccountnumberaccountnumber)
* [GET /appointments/:id](#get-appointmentsid)
* [PUT /appointments/:id](#put-appointmentsid)
* [DELETE /appointments/:id](#delete-appointmentsid)
* [Issues](#issues)
* [Authors](#authors)

### Overview
Appointments API allows you to manage appointments. Responses from this API will be returned in JSON format only.

### Appointment
Appointment as a resource represents following information

| Property | Type | Description |
| :-------------------- | :---------- | ------------------------------------------------------------ |
| id | string | `Returned always`. It is work request number to track the appointment. |
| serviceAccount | string | `Returned always`. It is account number of the appointment. |
| status | string | `Returned always`. It is the status of the appointment like `booked`, `engineer-preparing`, `engineer-on-the-way`, `completed`, `not-available`.|
| reason | string | `Returned always`. It is the type of the appointment. The possible reasons of appointment for a customer are `asv`, `fv`, `ib`, `asv-and-ib`, `fv-and-ib`.|
| trackable | boolean | `Returned always`. It is the flag to determine whether the job tracking can be displayed. |
| reschedulable | boolean | `Returned always`. It is the flag to identify reschedule option for the appointment |
| cancellable | boolean | `Returned always`. It is the flag to identify cancel option for the appointment |
| telephoneNumber | String | `Returned always`. It is the contact number for the appointment |
| slot | String | `Returned always`. It is the id of the slot mapped to this appointment |
| priority | boolean | `Returned always`. It represents the priority of the appointment |
| faults | Array of String | `Returned always`. It is list of faults for the appointment |

#### Slot
Slot as a resource will be represented as below:

| Property | Type | Description |
| :-------------------- | :---------- | ------------------------------------------------------------ |
| id | string | `Returned always`. Unique Id to represent the appointment slot with pattern date-starttime-endtime |
| date | string | `Returned always`. Date of the appointment slot |
| variant | String | `Returned always`. Slots type of the appointment slot  |
| startTime | String | `Returned always`. Start time of the appointment slot  |
| endTime | String | `Returned always`. End time of the appointment slot |
| available | boolean |  `Returned always`. Available status of the appointment slot |
| preferredSlot | boolean | `Returned always`. Preferred status of appointment slot  |

#### Fault
Fault as a resource will be represented as below:

| Property | Type | Description |
| :-------------------- | :---------- | ------------------------------------------------------------ |
| id | string | `Returned always`. It is the code for the fault |
| description | string | `Returned always`. It describes the fault of an appliance |

### GET /appointments
API Service returns all the appointments for the customer logged in

```http
GET /appointments
Authorization: Bearer accesstoken
cid: {clientid}
```
#### Parameters
No parameters required for fetching the appointment resource.

#### Response

```
Status: 200 OK
Content-Type: application/json
```
```json
{
    "status": "SUCCESS",
    "data": {
        "appointments": [
            {
                "id": "567891011",
                "serviceAccount": "919918239012",
                "status": "booked",
                "reason": "asv",
                "trackable": true,
                "reschedulable": true,
                "cancellable": true,
                "telephoneNumber": "0738123456",
                "slot": "2015-10-11T08:00:00+0100-2015-10-11T10:00:00+0100",
                "priority": false,
                "faults": [
                    "F0057",
                    "F0008"
                ]
            },
            {
                "id": "567891012",
                "serviceAccount": "919918239012",
                "status": "booked",
                "reason": "asv",
                "trackable": true,
                "reschedulable": true,
                "cancellable": true,
                "telephoneNumber": "0738123456",
                "slot": "2015-09-11T14:00:00+0100-2015-09-11T16:00:00+0100",
                "priority": false,
                "faults": [
                    "F0057"
                ]
            },
            {
                "id": "567891013",
                "serviceAccount": "919918239013",
                "status": "booked",
                "reason": "fv-and-ib",
                "trackable": true,
                "reschedulable": true,
                "cancellable": true,
                "telephoneNumber": "0738123456",
                "slot": "2015-10-11T14:00:00+0100-2015-10-11T16:00:00+0100",
                "priority": false,
                "faults": [
                    "F0007"
                ]
            }
        ],
        "slots": [
            {
                "id": "2015-10-11T08:00:00+0100-2015-10-11T10:00:00+0100",
                "date": null,
                "variant": null,
                "startTime": "2015-10-11T08:00:00+0100",
                "endTime": "2015-10-11T10:00:00+0100",
                "available": false,
                "preferredSlot": false
            },
            {
                "id": "2015-09-11T14:00:00+0100-2015-09-11T16:00:00+0100",
                "date": null,
                "variant": null,
                "startTime": "2015-09-11T14:00:00+0100",
                "endTime": "2015-09-11T16:00:00+0100",
                "available": false,
                "preferredSlot": false
            },
            {
                "id": "2015-10-11T14:00:00+0100-2015-10-11T16:00:00+0100",
                "date": null,
                "variant": null,
                "startTime": "2015-10-11T14:00:00+0100",
                "endTime": "2015-10-11T16:00:00+0100",
                "available": false,
                "preferredSlot": false
            }
        ],
        "faults": [
            {
                "id": "F0057",
                "description": "Fusebox damaged"
            },
            {
                "id": "F0008",
                "description": "Unknown fault"
            },
            {
                "id": "F0007",
                "description": "Problem with Time Clock"
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
    "errors": [
        {
            "code": "authorize",
            "message": "access_denied"
        }
    ],
    "meta": {}
}
```
##### Case 2: Appointment not found
When there are no appointments booked or request for a customer who dont have service accounts, API responses with following

```
Status: 404 Not Found 
Content-Type: application/json
```
```json
{
    "status": "FAIL",
    "data": {},
    "errors": [
        {
            "code": "appointment",
            "message": "error.client.appointment.notFound"
        }
    ],
    "meta": {}
}
```
##### Case 3: Error from SAP
When any error occured, API responses with following

```
Status: 500 Error 
Content-Type: application/json
```
```json
{
    "status": "ERROR",
    "data": {},
    "errors": [
        {
            "code": "service",
            "message": "error.system.pi.operation.fail"
        }
    ],
    "meta": {}
}
```

### GET /appointments?accountNumber=:accountNumber...
API Service returns all the appointments for an account(s) belonging to the logged in customer

```http
GET /appointments?accountNumber={accountNumber1}&accountNumber={accountNumber2}
Authorization: Bearer accesstoken
cid: {clientid}
```
#### Parameters
No parameters required for fetching the appointment resource.

#### Response

```
Status: 200 OK
Content-Type: application/json
```
```json
{
    "status": "SUCCESS",
    "data": {
        "appointments": [
            {
                "id": "567891011",
                "serviceAccount": "919918239012",
                "status": "booked",
                "reason": "asv",
                "trackable": true,
                "reschedulable": true,
                "cancellable": true,
                "telephoneNumber": "0738123456",
                "slot": "2015-10-11T08:00:00+0100-2015-10-11T10:00:00+0100",
                "priority": false,
                "faults": [
                    "F0057",
                    "F0008"
                ]
            },
            {
                "id": "567891012",
                "serviceAccount": "919918239012",
                "status": "booked",
                "reason": "asv-and-ib",
                "trackable": true,
                "reschedulable": true,
                "cancellable": true,
                "telephoneNumber": "0738123456",
                "slot": "2015-09-11T14:00:00+0100-2015-09-11T16:00:00+0100",
                "priority": false,
                "faults": [
                    "F0008"
                ]
            }
        ],
        "slots": [
            {
                "id": "2015-10-11T08:00:00+0100-2015-10-11T10:00:00+0100",
                "date": null,
                "variant": null,
                "startTime": "2015-10-11T08:00:00+0100",
                "endTime": "2015-10-11T10:00:00+0100",
                "available": false,
                "preferredSlot": false
            },
            {
                "id": "2015-09-11T14:00:00+0100-2015-09-11T16:00:00+0100",
                "date": null,
                "variant": null,
                "startTime": "2015-09-11T14:00:00+0100",
                "endTime": "2015-09-11T16:00:00+0100",
                "available": false,
                "preferredSlot": false
            }
        ],
        "faults": [
            {
                "id": "F0057",
                "description": "Fusebox damaged"
            },
            {
                "id": "F0008",
                "description": "Unknown fault"
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
    "errors": [
        {
            "code": "authorize",
            "message": "access_denied"
        }
    ],
    "meta": {}
}
```
##### Case 2: AccountNumber is invalid
When you request with an invalid accountNumber or non service account number, API responses with following

```
Status: 400 Bad Request 
Content-Type: application/json
```
```json
{
    "status": "FAIL",
    "data": {},
    "errors": [
        {
            "code": "accountNumber",
            "message": "error.client.accountNumber.invalid"
        }
    ],
    "meta": {}
}
```
##### Case 3: Account is not available for the customer
When you request an accountNumber which is not part of the customer, API responses with following

```
Status: 401 Authorization Required 
Content-Type: application/json
```
```json
{
    "status": "FAIL",
    "data": {},
    "errors": [
        {
            "code": "accountNumber",
            "message": "error.client.accountNumber.invalid"
        }
    ],
    "meta": {}
}
```
##### Case 4: Appointment not found
When request an account number for a customer who dont have service accounts or there are no appointments booked, API responses with following

```
Status: 404 Not Found 
Content-Type: application/json
```
```json
{
    "status": "FAIL",
    "data": {},
    "errors": [
        {
            "code": "appointment",
            "message": "error.client.appointment.notFound"
        }
    ],
    "meta": {}
}
```

##### Case 5: Error from SAP
When any error occured, API responses with following

```
Status: 500 Error 
Content-Type: application/json
```
```json
{
    "status": "ERROR",
    "data": {},
    "errors": [
        {
            "code": "service",
            "message": "error.system.pi.operation.fail"
        }
    ],
    "meta": {}
}
```

### GET /appointments/:id
API Service returns a specific appointment selected using the id, which is available for the customer logged in

```http
GET /appointments/{appointmentId}
Authorization: Bearer accesstoken
cid: {clientid}
```
#### Parameters
No parameters required for fetching the appointment resource.

#### Response

```
Status: 200 OK
Content-Type: application/json
```
```json
{
    "status": "SUCCESS",
    "data": {
        "appointment": {
            "id": "567891011",
            "serviceAccount": "919918239012",
            "status": "booked",
            "reason": "asv",
            "trackable": true,
            "reschedulable": true,
            "cancellable": true,
            "telephoneNumber": "0738123456",
            "slot": "2015-10-11T08:00:00+0100-2015-10-11T10:00:00+0100",
            "priority": false,
            "faults": [
                "F0057",
                "F0008"
            ]
        },
        "slot": {
            "id": "2015-10-11T08:00:00+0100-2015-10-11T10:00:00+0100",
            "date": null,
            "variant": null,
            "startTime": "2015-10-11T08:00:00+0100",
            "endTime": "2015-10-11T10:00:00+0100",
            "available": false,
            "preferredSlot": false
        },
        "faults": [
            {
                "id": "F0057",
                "description": "Fusebox damaged"
            },
            {
                "id": "F0008",
                "description": "Unknown fault"
            }
        ]
    },
    "errors": [],
    "meta": {}
}
```
#### Possible Errors
##### Case 1: Appointment not found
When request for a customer who dont have service accounts or there are no appointments booked, API responses with following

```
Status: 404 Not Found 
Content-Type: application/json
```
```json
{
    "status": "FAIL",
    "data": {},
    "errors": [
        {
            "code": "appointment",
            "message": "error.client.appointment.notFound"
        }
    ],
    "meta": {}
}
```
##### Case 2: Error from SAP
When any error occured, API responses with following

```
Status: 500 Error 
Content-Type: application/json
```
```json
{
    "status": "ERROR",
    "data": {},
    "errors": [
        {
            "code": "service",
            "message": "error.system.pi.operation.fail"
        }
    ],
    "meta": {}
}
```
### PUT /appointments/:id
API Service helps to reschudele a specific appointment, which is available for the customer logged in

```http
PUT /appointments/{appointmentId}
Authorization: Bearer accesstoken
cid: {clientid}
```
API Service helps to reschedule a specific appointment, which is available for the customer logged in

#### Request

```json
{
    "appointment": {
        "id": "567891011",
        "serviceAccount": "919918239012",
        "status": "Booked",
        "reason": "ASV",
        "trackable": true,
        "reschedulable": true,
        "cancellable": true,
        "telephoneNumber": "0738123456",
        "slot": "2015-12-11T08:00:00+0100-2015-12-11T10:00:00+0100",
        "priority": false,
        "faults": [
            "F0057",
            "F0008"
        ]
    }
}
```
#### Response

```
Status: 200 OK
Content-Type: application/json
```
```json

{
    "status": "SUCCESS",
    "data": {
        "appointment": {
            "id": "567891011",
            "serviceAccount": "919918239012",
            "status": "Booked",
            "reason": "ASV",
            "trackable": true,
            "reschedulable": true,
            "cancellable": true,
            "telephoneNumber": "0738123456",
            "slot": "2015-12-11T08:00:00+0100-2015-12-11T10:00:00+0100",
            "priority": false,
            "faults": [
                "F0057",
                "F0008"
            ]
        }
    },
    "errors": [],
    "meta": {}
}
```

#### Possible Errors

##### Case 1: Appointment slot is invalid
When the appointment resource input has an empty slot, API response with following

```
Status: 400 Bad Request 
Content-Type: application/json
```

```json
{
    "status": "FAIL",
    "data": {},
    "errors": [
        {
            "code": "slot",
            "message": "error.client.slot.invalid"
        }
    ],
    "meta": {}
}
```

##### Case 2: Appointment telephone number is invalid
When the appointment resource input has an empty telephone number, API response with following

```
Status: 400 Bad Request 
Content-Type: application/json
```
```json
{
    "status": "FAIL",
    "data": {},
    "errors": [
        {
            "code": "telephoneNumber",
            "message": "error.client.telephoneNumber.invalid"
        }
    ],
    "meta": {}
}
```
##### Case 3: Appointment id is invalid
When the requested id is not matching with the id in the request, API response with following

```
Status: 400 Bad Request 
Content-Type: application/json
```
```json
{
    "status": "FAIL",
    "data": {},
    "errors": [
        {
            "code": "id",
            "message": "error.client.id.invalid"
        }
    ],
    "meta": {}
}
```
##### Case 4: Appointment not found
When there are no appointments booked, API responses with following

```
Status: 404 Not Found 
Content-Type: application/json
```
```json
{
    "status": "FAIL",
    "data": {},
    "errors": [
        {
            "code": "appointment",
            "message": "error.client.appointment.notFound"
        }
    ],
    "meta": {}
}
```
##### Case 5: Appointment resource is not modified
When the requested appointment resource is not modified, API responses with following

```
Status: 400 Bad Request 
Content-Type: application/json
```
```json
{
    "status": "FAIL",
    "data": {},
    "errors": [
        {
            "code": "appointment",
            "message": "error.client.appointment.notModified"
        }
    ],
    "meta": {}
}
```

##### Case 6: Invalid modification on Appointment resource
When the invalid modification done to the appointment resource requested, API responses with following

```
Status: 400 Bad Request 
Content-Type: application/json
```
```json
{
    "status": "FAIL",
    "data": {},
    "errors": [
        {
            "code": "appointment",
            "message": "error.client.appointment.modificationNotAllowed"
        }
    ],
    "meta": {}
}
```

##### Case 7: Appointment slot is not available
When the selected slot to reschdule is not available, API responses with following

```
Status: 400 Bad Request 
Content-Type: application/json
```
```json
{
    "status": "FAIL",
    "data": {},
    "errors": [
        {
            "code": "slot",
            "message": "error.client.slot.unavailable"
        }
    ],
    "meta": {}
}
```

##### Case 8: Error from SAP
When any error occured, API responses with following

```
Status: 500 Error 
Content-Type: application/json
```
```json
{
    "status": "ERROR",
    "data": {},
    "errors": [
        {
            "code": "service",
            "message": "error.system.pi.operation.fail"
        }
    ],
    "meta": {}
}
```

### DELETE /appointments/:id
API Service helps to cancel a specific appointment, which is available for the customer logged in

```http
DELETE /appointments/{appointmentId}
Authorization: Bearer accesstoken
cid: clientid
```

#### Parameters
No parameters required for fetching the appointment resource.

#### Response

```http
Status: 204 No Content
Content-Type: application/json
```

#### Possible Errors
##### Case 1: Appointment not found
When there are no appointments booked, API responses with following

```
Status: 404 Not Found 
Content-Type: application/json
```
```json
{
    "status": "FAIL",
    "data": {},
    "errors": [
        {
            "code": "appointment",
            "message": "error.client.appointment.notFound"
        }
    ],
    "meta": {}
}
```

##### Case 2: Appointment Id is invalid
When the appointment Id is not passed as a path parameter, API responses with following

```
Status: 400 Bad Request 
Content-Type: application/json
```
```json
{
    "status": "FAIL",
    "data": {},
    "errors": [
        {
            "code": "id",
            "message": "error.client.id.blank"
        }
    ],
    "meta": {}
}
```
##### Case 3: Error from SAP
When any error occured, API responses with following

```
Status: 500 Error 
Content-Type: application/json
```
```json
{
    "status": "ERROR",
    "data": {},
    "errors": [
        {
            "code": "service",
            "message": "error.system.pi.operation.fail"
        }
    ],
    "meta": {}
}
```
### Issues
* No known issues at this moment

### Authors
@GiritharanR
