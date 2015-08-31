#Summary
This chapter show oceanclouds self used API.

* [Get App Auth Code](#Get App Auth Code)
* [Subscribe Service](#Subscribe Service)
* [Cancel Service](#Cancel Service)
* [Get Subscribed Services](#Get Subscribed Services)


<a name="Get App Auth Code"></a>
### Get App Auth Code

Call this API to get a expire in 60 seconds auth code, this auth code can be used to fetch app info through back service [Get App By Auth Code](./api_for_backservice.md#Get App By Auth Code) API.

**Service Request**

> GET https://api.oceanclouds.com/v1.0/app/auth_code

**Input**

Empty.

**Output**

Entities is array of 

| Entity key | description |
|:-|:-|
|_id|Subscribed back service id.|
|key|Back service key.|
|name|Back service name.|
|description|Back service description.|
|status|Back service subscribe status.|


**Sample**

Output is 

```json
{
  "success": true,
  "entity": {
    "__v": 0,
    "authCode": "0efc46c1584e5d51c58a0f3317491f09f9047c55",
    "resourceId": "55b88eef4df03bab3307c0ff",
    "resourceKey": "test_app",
    "type": "app",
    "expireTime": 1438160215054,
    "expired": false,
    "_id": "55b8951b4df03bab3307c102"
  }
}
```

<a name="Subscribe Service"></a>
### Subscribe Service

**Service Request**

> POST https://api.oceanclouds.com/v1.0/app/service/:backServiceId/subscribe

**Input**

Empty.

**Output**

No entity.

**Sample**
POST https://api.oceanclouds.com/v1.0/app/service/55b74c844df03bab3307c0bf/subscribe

Output is

```json
{
  "success":true
}
```

<a name="Cancel Service"></a>
### Cancel Service

**Service Request**

> POST https://api.oceanclouds.com/v1.0/app/service/:backServiceId/cancel

**Input**

Empty.

**Output**

No entity.

**Sample**

POST https://api.oceanclouds.com/v1.0/app/service/55b74c844df03bab3307c0bf/cancel

Output is

```json
{
  "success":true
}
```

<a name="Get Subscribed Services"></a>
### Get Subscribed Services

**Service Request**

> GET https://api.oceanclouds.com/v1.0/app/subscribed_services

**Input**

Empty.

**Output**

Entities is array of 

| Entity key | description |
|:-|:-|
|_id|Subscribed back service id.|
|key|Back service key.|
|name|Back service name.|
|description|Back service description.|
|status|Back service subscribe status. The status are *subscribed*,*pending_subscribed* , *pending_cancel*|


**Sample**

Output is 

```json
{
  "success": true,
  "rows": 1,
  "entities": [
    {
      "status": "subscribed",
      "_id": "55b74c844df03bab3307c0bf",
      "key": "crud",
      "name": "Data Persistent Service (Mongo DB)",
      "description": "Data Persistent Service provide data create, read, update, delete, query service."
    }
  ]
}
```

