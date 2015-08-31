#Summary

* [Passport](#Ocean Passport)
	* [Register](#Register)
	* [Login](#Login)
* [Public Resource](#Public Resource)
	* [Query Public Back Services](#Query Public Back Services)
	* [Query Public Applications](#Query Public Applications)


<a name="Ocean Passport"></a>
## Ocean Passport

<a name="Register"></a>
### Register

**Service Request**

> POST https://api.oceanclouds.com/v1.0/public/register

**Input**

| key | description |
|:-|:-|
|email|Account email address|
|password|Account password|
|cellphone|Account cellphone, can be only bind to one account|
|displanName|Account screen name|
|invitationCode|Invitation code from oceanclouds|

**Output**

Entity is 

| Entity key | description |
|:-|:-|
|email|Account email address|
|password|Account password|
|cellphone|Account cellphone, can be only bind to one account|
|displanName|Account screen name|
|invitationCode|Invitation code from oceanclouds|

API Error

|ErrorCode|Description|
|:-|:-|
|passport.invitationNotRight|Your invitation code can not be found or already be used!|
|passport.emailAlreadyExist|User email is already used by another account!|
|passport.emailFormatNotRight|User account email format is not right!|
|passport.cellPhoneFormatNotRight|User account cellphone format is not right!|



**Sample**

Input is 
```json
{
  "email": "test@oceanclouds.com",
  "password": "123456",
  "cellphone":"",
  "displayName":"Test Account",
  "invitationCode":"b014272692f760011"
}
```

Output is 

```json
{
  "success": true,
  "entity": {
    "__v": 0,
    "email": "test@oceanclouds.com",
    "password": "********",
    "cellphone": "",
    "displayName": "Test Account",
    "invitationCode": "b014272692f760011",
    "_id": "55b843a84df03bab3307c0fa"
  }
}
```

<a name="Login"></a>
### Login

**Service Request**

> POST https://api.oceanclouds.com/v1.0/public/login

**Input**

| key | description |
|:-|:-|
|email|Account email|
|password|Account password|
|remember|True or false, if true will get 30 days developer access token|

**Output**

This call will return a array of access tokens which are binding to this developer.

AccessToken entity is 

| Entity key | description |
|:-|:-|
|accessTokenCode|Account email address|
|type|Account email address|
|userAccountId|Developer id|
|resourceKey|Access token target resource key(app or backservice is key, developer is email)|
|resourceId|Access token target resource id|
|expireTime|In which time access token will expire|
|expired|If this access token is expired|


API Error

|ErrorCode|Description|
|:-|:-|
|passport.noAccount|User account can not be found!!|
|passport.loginFailed|User accountName or password not right!|


**Sample**

Input Body is

```json
{
  "email": "test@oceanclouds.com",
  "password": "123456",
  "remember":false
}
```
Output body is 

```json
{
  "success": true,
  "rows": 1,
  "entities": [
    {
      "_id": "55b844354df03bab3307c0fb",
      "accessTokenCode": "24c96637bda40bd01e72c68bbbc03bc98134b69a",
      "type": "developer",
      "userAccountId": "55b843a84df03bab3307c0fa",
      "resourceKey": "test@oceanclouds.com",
      "resourceId": "55b843a84df03bab3307c0fa",
      "expireTime": 1438225845487,
      "__v": 0,
      "expired": false
    }
  ]
}
```

<a name="Public Resource"></a>
## Public Resource
<a name="Query Public Back Services"></a>
### Query Public Back Services

**Service Request**

> GET https://api.oceanclouds.com/v1.0/public/services

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


**Sample**

Input is empty.

Output is 

```json
{
  "success": true,
  "rows": 4,
  "entities": [
    {
      "_id": "55b74c844df03bab3307c0bf",
      "key": "crud",
      "name": "Data Persistent Service (Mongo DB)",
      "description": "Data Persistent Service provide data create, read, update, delete, query service."
    },
    {
      "_id": "55b74cb94df03bab3307c0c1",
      "key": "user",
      "name": "Basic User Auth Service",
      "description": "Basic user service provide user register, login api service for integration ocean clouds platform."
    },
    {
      "_id": "55b74ce84df03bab3307c0c3",
      "key": "weibo",
      "name": "Weibo user auth service",
      "description": "This service provide user authentication service from sina weibo."
    },
    {
      "_id": "55b74d154df03bab3307c0c5",
      "key": "facebook",
      "name": "Facebook user auth service",
      "description": "This service provide facebook oauth login and authorize service."
    }
  ]
}
```

<a name="Query Public Applications"></a>
### Query Public Applications

**Service Request**

> GET https://api.oceanclouds.com/v1.0/public/apps

**Input**

Empty.

**Output**

Entities is array of 

| Entity key | description |
|:-|:-|
|_id|Subscribed back service id.|
|key|Application key.|
|name|Application name.|
|description|Application description.|


**Sample**

Input is empty.

Output is 

```json
{
  "success": true,
  "rows": 2,
  "entities": [
    {
      "_id": "55b74e734df03bab3307c0c7",
      "key": "sample_app",
      "name": "Sample blog app"
    },
    {
      "_id": "55b74e854df03bab3307c0c9",
      "key": "mypenpal",
      "name": "My pen pal website"
    }
  ]
}
```




