#Summary
This chapter show oceanclouds back service use API. These API is protected by service access token, so when visit, you need to fill your service access token in HTTP AccessToken header.


* [Message](#Message)
	* [Get Messages](#Get Messages)
	* [Get Message](#Get Message)
	* [Resolve Message](#Resolve Message)
* [Application](#Application)
	* [Get App By Id](#Get App By Id)
	* [Get App By Auth Code](#Get App By Auth Code)
* [App User](#App User)
	* [Create App User](#Create App User)
	* [Update App User](#Update App User)
	* [Get App User Access Token](#Get App User Access Token)




<a name="Message"></a>
## Message

Ocean use message to transfer information to back service, for now, only some application subscribe or cancel your back service, a message will generate, you need to deal with ocean message.

<a name="Get Messages"></a>
### Get Messages

**Service Request**

> GET https://api.oceanclouds.com/v1.0/service/messages

**Input**
Empty

**Output**

Entity is 

| key | description |
|:-|:-|
|type|Message type. Including *app_subscribe_service*, *app_cancel_service*|
|content|Message content.|
|status|Message status. Including *init*,*send*,*resolved*|

**Sample**

out put is
```json
{
  "success": true,
  "rows": 1,
  "entities": [
    {
      "_id": "55b89ba34df03bab3307c10f",
      "backServiceId": "55b89b274df03bab3307c10c",
      "type": "app_subscribe_service",
      "content": "{\"appId\":\"55b88eef4df03bab3307c0ff\",\"appKey\":\"test_app\",\"appSubscriptionId\":\"55b89ba34df03bab3307c10e\"}",
      "status": "init",
      "__v": 0
    }
  ]
}
```

<a name="Get Message"></a>
### Get Message

**Service Request**

> GET https://api.oceanclouds.com/v1.0/service/message/:messageId

**Input**
Empty

**Output**

Entity is 

| key | description |
|:-|:-|
|type|Message type. Including *app_subscribe_service*, *app_cancel_service*|
|content|Message content.|
|status|Message status. Including *init*,*send*,*resolved*|

**Sample**

GET https://api.oceanclouds.com/v1.0/service/message/55b89ba34df03bab3307c10f

out put is
```json
{
  "success": true,
  "entity": {
    "_id": "55b89ba34df03bab3307c10f",
    "backServiceId": "55b89b274df03bab3307c10c",
    "type": "app_subscribe_service",
    "content": "{\"appId\":\"55b88eef4df03bab3307c0ff\",\"appKey\":\"test_app\",\"appSubscriptionId\":\"55b89ba34df03bab3307c10e\"}",
    "status": "init",
    "__v": 0
  }
}
```

<a name="Resolve Message"></a>
### Resolve Message

**Service Request**

> POST https://api.oceanclouds.com/v1.0/service/message/:messageId/resolved

**Input**
Empty

**Output**

No Entity.

**Sample**

POST https://api.oceanclouds.com/v1.0/service/message/55b89ba34df03bab3307c10f/resolved

out put is
```json
{
  "success": true
}
```

<a name="Application"></a>
## Application

<a name="Get App By Id"></a>
### Get App By Id

This API can only visit the appId which subscribed your back service.

**Service Request**

> GET https://api.oceanclouds.com/v1.0/service/app/:appId

**Input**

Empty.

**Output**

AccessToken entity is 

| Entity key | description |
|:-|:-|
|name|App Name|
|key|App Key|


**Sample**

Output is

```json
{
  "success": true,
  "entity": {
    "_id": "55b88eef4df03bab3307c0ff",
    "name": "Test_App",
    "key": "test_app"
  }
}
```

<a name="Get App By Auth Code"></a>
### Get App By Auth Code

This API can only visit the appId which subscribed your back service.

**Service Request**

> GET https://api.oceanclouds.com/v1.0/service/app/by_auth_code/:authCode

**Input**

Empty.

**Output**

AccessToken entity is 

| Entity key | description |
|:-|:-|
|name|App Name|
|key|App Key|

Errors

|ErrorCode|Description|
|:-|:-|
|authCode.NotExist|Auth code not exist!|
|authCode.Expired|Auth code already expired!|
|authCode.TypeNotRight|You may use the wrong auth code type to access resource!|

**Sample**

Output is

```json
{
  "success": true,
  "entity": {
    "_id": "55b88eef4df03bab3307c0ff",
    "name": "Test_App",
    "key": "test_app"
  }
}
```

<a name="App User"></a>
## App User

These API is controlled by back service field **allowUserApi** , only used by app user auth back service.

<a name="Create App User"></a>
### Create App User

**Service Request**

> POST https://api.oceanclouds.com/v1.0/service/app/:appId/users

**Input**

| Entity key | description |
|:-|:-|
|accountName|Account name(unique for your back service)|
|displayName|Account display name|
|email|Account email, optional.|
|cellphone|Account cellphone, optional.|

**Output**

AccessToken entity is 

| Entity key | description |
|:-|:-|
|accountName|Account name(unique for your back service)|
|displayName|Account display name|
|email|Account email, optional.|
|cellphone|Account cellphone, optional.|

**Sample**

Input is 
{
    "accountName":"test_app_user",
    "displayName":"张三",
    "email":"test@atest.com",
    "cellphone":""
}


Output is

```json
{
  "success": true,
  "entity": {
    "__v": 0,
    "_id": "55b891fb4df03bab3307c101",
    "accountName":"test_app_user",
    "displayName":"张三",
    "email":"test@atest.com",
    "cellphone":"",
    "createTime": 1438157084000,
    "updateTime": 1438157084000,
    "createBy": "55b843a84df03bab3307c0fa",
    "updateBy": "55b843a84df03bab3307c0fa"
  }
}
```

<a name="Update App User"></a>
### Update App User

**Service Request**

> PUT https://api.oceanclouds.com/v1.0/service/app/:appId/user/:appUserId

**Input**

| Entity key | description |
|:-|:-|
|displayName|Account display name|
|email|Account email, optional.|
|cellphone|Account cellphone, optional.|

**Output**

AccessToken entity is 

| Entity key | description |
|:-|:-|
|accountName|Account name(unique for your back service)|
|displayName|Account display name|
|email|Account email, optional.|
|cellphone|Account cellphone, optional.|

**Sample**

Input is 
{
    "displayName":"张三",
    "email":"test@atest.com",
    "cellphone":""
}


Output is

```json
{
  "success": true,
  "entity": {
    "__v": 0,
    "_id": "55b891fb4df03bab3307c101",
    "accountName":"test_app_user",
    "displayName":"张三",
    "email":"test@atest.com",
    "cellphone":"",
    "createTime": 1438157084000,
    "updateTime": 1438157123000,
    "createBy": "55b843a84df03bab3307c0fa",
    "updateBy": "55b843a84df03bab3307c0fa"
  }
}
```

<a name="Get App User Access Token"></a>
### Get App User Access Token

**Service Request**

> GET https://api.oceanclouds.com/v1.0/service/app/:appId/user/:appUserId/access_token

**Input**

Empty.

**Output**

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

**Sample**

Output is

```json
{
  "success": true,
  "entity": {
    "__v": 0,
    "accessTokenCode": "d56578cabced0b35683bc964022d1a6f5fcd9a99",
    "type": "end",
    "userAccountId": "",
    "resourceKey": "test",
    "resourceId": "55b88eef4df03bab3307c0ff",
    "expireTime": 1440751355191,
    "_id": "55b891fb4df03bab3307c101",
    "expired": false
  }
}
```


