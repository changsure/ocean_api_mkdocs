#Summary
This chapter show oceanclouds developer use API. These API is protected by developer access token, so when visit, you need to fill your developer access token in HTTP AccessToken header.

* [Developer Account](#Developer Account)
	* [Get My Account Info](#Get My Account Info)
	* [Update My Account Info](#Update My Account Info)
* [BackService Manage](#BackService Manage)
	* [Create Back Service](#Create Back Service)
	* [Read Back Service](#Read Back Service)
	* [Read Back Services](#Read Back Services)
	* [Update Back Service](#Update Back Service)
	* [Delete Back Service](#Delete Back Service)	
* [App Manage](#App Manage)
	* [Create App](#Create App)
	* [Read App](#Read App)
	* [Read Apps](#Read Apps)
	* [Update App](#Update App)
	* [Delete App](#Delete App)
* [Access Token](#Access Token)
	* [Get Access Tokens](#Get Access Tokens)
	* [Get Access Token](#Get Access Token)
	* [Regenerate Access Token](#Regenerate Access Token)


<a name="Developer Account"></a>
## Developer Account

<a name="Get My Account Info"></a>
### Get My Account Info

**Service Request**

> GET https://api.oceanclouds.com/v1.0/developer/me

**Input**

Empty.

**Output**

Developer account entity is 

| Entity key | description |
|:-|:-|
|email|Account email address|
|password|Return with 8 *|
|cellphone|Account cellphone, can be only bind to one account|
|displanName|Account screen name|
|invitationCode|Invitation code from oceanclouds|


**Sample**

Output is 

```json
{
  "success": true,
  "entity": {
    "_id": "55b843a84df03bab3307c0fa",
    "email": "test@oceanclouds.com",
    "password": "********",
    "cellphone": "",
    "displayName": "Test Account",
    "invitationCode": "b014272692f760011",
    "__v": 0
  }
}
```

<a name="Update My Account Info"></a>
### Update My Account Info

**Service Request**

> PUT https://api.oceanclouds.com/v1.0/developer/me

**Input**

Developer account

| Entity key | description |
|:-|:-|
|password|Your new password|
|cellphone|Account cellphone, can be only bind to one account|
|displanName|Account screen name|


**Output**

Developer account entity is 

| Entity key | description |
|:-|:-|
|email|Account email address|
|password|Return with 8 *|
|cellphone|Account cellphone, can be only bind to one account|
|displanName|Account screen name|
|invitationCode|Invitation code from oceanclouds|

**Sample**

Input Body is

```json
{
    "password": "654321",
    "cellphone": "15612320934",
    "displayName": "Test Account"
}
```
Output body is 

```json
{
  "success": true,
  "entity": {
    "_id": "55b843a84df03bab3307c0fa",
    "email": "test@oceanclouds.com",
    "password": "********",
    "cellphone": "15612320934",
    "displayName": "Test Account",
    "invitationCode": "b014272692f760011",
    "__v": 0,
    "updateTime": 1438156662000,
    "updateBy": "55b843a84df03bab3307c0fa"
  }
}
```


<a name="BackService Manage"></a>
## BackService Manage

This api need oceanclouds account to login first, will check *account passport cookie* first.

<a name="Create Back Service"></a>
### Create Back Service

**Service Request**

> POST https://api.oceanclouds.com/v1/ocean/backServiceManage/backServices

**Input**

Entity

| Entity key | description |
|:-|:-|
|key|Back service key. Every back service have an individual key and it's unique in oceanclouds.|
|name|Back service name.|
|type|Here only accept PRIVATE.|
|signKey|A secure key for exchange message between app end user and back service. |
|messageApiAddress|Api address for receiving oceanclouds message.|
|serviceApiAddress|Api root address for app. |
|description| Description about this back service. |
|manageAddress|Your back service manage console address, this address should accept a appAuthCode to identify which app is visiting.|
|manageByOpen|True or False, Should this manage console open by a new window in ocean UI.|
|allowUserApi|True or False, is this back service a user auth back service?|

**Output**

Entity

| Entity key | description |
|:-|:-|
|_id|Back service id.|
|key|Back service key. Every back service have an individual key and it's unique in oceanclouds.|
|name|Back service name.|
|type|PRIVATE or PUBLIC. A PUBLIC back service can be subscribe by any app, PRIVATE back service can only used by owner app. For now user only can request a PRIVATE back service.|
|signKey|A secure key for exchange message between Oceanclouds and back service. |
|messageApiAddress|Api address for receiving oceanclouds message.|
|serviceApiAddress|Api root address for app. |
|description| Description about this back service. |
|createTime|Create time(Unix time millisecond) of this back service. |
|updateTime|Update time(Unix time millisecond) of this back service.|
|createBy|Create account ID.|
|updateBy|Update account ID.|
|ownerId|Owner account ID.|
|manageAddress|Your back service manage console address, this address should accept a appAuthCode to identify which app is visiting.|
|manageByOpen|Should this manage console open by a new window in ocean UI.|
|allowUserApi|Is this back service a user auth back service?|

**Sample**

Input is 

```json
{
  "name": "TestService",
  "key": "sample_test",
  "messageApiAddress":"https://localhost/api/message",
  "signKey":"sample_signKey",
  "serviceApiAddress": "https://localhost/api/service",
  "description":"This is a test back service.",
  "type":"PRIVATE",
  "manageAddress":"https://localhost/console",
  "manageByOpen":false,
  "allowUserApi":false
}
```

Output is 

```json
{
  "success": true,
  "entity": {
    "__v": 0,
    "name": "TestService",
    "key": "sample_test",
    "messageApiAddress": "https://localhost/api/message",
    "signKey": "sample_signKey",
    "serviceApiAddress": "https://localhost/api/service",
    "description": "This is a test back service.",
    "type": "PRIVATE",
    "manageAddress": "https://localhost/console",
    "createTime": 1438157084000,
    "updateTime": 1438157084000,
    "createBy": "55b843a84df03bab3307c0fa",
    "updateBy": "55b843a84df03bab3307c0fa",
    "ownerId": "55b843a84df03bab3307c0fa",
    "_id": "55b8891c4df03bab3307c0fd",
    "allowUserApi": false,
    "manageByOpen": false
  }
}
```

<a name="Read Back Service"></a>
### Read Back Service

**Service Request**

> GET https://api.oceanclouds.com/v1.0/developer/service/:backServiceId

**Input**

Empty.

**Output**

Back Service Entity is 

| Entity key | description |
|:-|:-|
|_id|Back service id.|
|key|Back service key. Every back service have an individual key and it's unique in oceanclouds.|
|name|Back service name.|
|type|PRIVATE or PUBLIC. A PUBLIC back service can be subscribe by any app, PRIVATE back service can only used by owner app. For now user only can request a PRIVATE back service.|
|signKey|A secure key for exchange message between Oceanclouds and back service. |
|messageApiAddress|Api address for receiving oceanclouds message.|
|serviceApiAddress|Api root address for app. |
|description| Description about this back service. |
|createTime|Create time(Unix time millisecond) of this back service. |
|updateTime|Update time(Unix time millisecond) of this back service.|
|createBy|Create account ID.|
|updateBy|Update account ID.|
|ownerId|Owner account ID.|
|manageAddress|Your back service manage console address, this address should accept a appAuthCode to identify which app is visiting.|
|manageByOpen|Should this manage console open by a new window in ocean UI.|
|allowUserApi|Is this back service a user auth back service?|


**Sample**

GET https://api.oceanclouds.com/v1.0/developer/service/55b8891c4df03bab3307c0fd
Input body is Empty.

Output body is

```json
{
  "success": true,
  "entity": {
    "_id": "55b8891c4df03bab3307c0fd",
    "name": "TestService",
    "key": "sample_test",
    "messageApiAddress": "https://localhost/api/message",
    "signKey": "sample_signKey",
    "serviceApiAddress": "https://localhost/api/service",
    "description": "This is a test back service.",
    "type": "PRIVATE",
    "manageAddress": "https://localhost/console",
    "createTime": 1438157084000,
    "updateTime": 1438157084000,
    "createBy": "55b843a84df03bab3307c0fa",
    "updateBy": "55b843a84df03bab3307c0fa",
    "ownerId": "55b843a84df03bab3307c0fa",
    "__v": 0,
    "allowUserApi": false,
    "manageByOpen": false
  }
}
```

<a name="Read Back Services"></a>
### Read Back Services

**Service Request**

> GET https://api.oceanclouds.com/v1.0/developer/services

**Input**

Empty.

**Output**

Entities is array of 

| Entity key | description |
|:-|:-|
|_id|Back service id.|
|key|Back service key. Every back service have an individual key and it's unique in oceanclouds.|
|name|Back service name.|
|type|PRIVATE or PUBLIC. A PUBLIC back service can be subscribe by any app, PRIVATE back service can only used by owner app. For now user only can request a PRIVATE back service.|
|signKey|A secure key for exchange message between Oceanclouds and back service. |
|messageApiAddress|Api address for receiving oceanclouds message.|
|serviceApiAddress|Api root address for app. |
|description| Description about this back service. |
|createTime|Create time(Unix time millisecond) of this back service. |
|updateTime|Update time(Unix time millisecond) of this back service.|
|createBy|Create account ID.|
|updateBy|Update account ID.|
|ownerId|Owner account ID.|
|manageAddress|Your back service manage console address, this address should accept a appAuthCode to identify which app is visiting.|
|manageByOpen|Should this manage console open by a new window in ocean UI.|
|allowUserApi|Is this back service a user auth back service?|


**Sample**

Input body is Empty.

Output body is

```json
{
  "success": true,
  "rows": 1,
  "entities": [
    {
      "_id": "55b8891c4df03bab3307c0fd",
      "name": "TestService",
      "key": "sample_test",
      "messageApiAddress": "https://localhost/api/message",
      "signKey": "sample_signKey",
      "serviceApiAddress": "https://localhost/api/service",
      "description": "This is a test back service.",
      "type": "PRIVATE",
      "manageAddress": "https://localhost/console",
      "createTime": 1438157084000,
      "updateTime": 1438157713000,
      "createBy": "55b843a84df03bab3307c0fa",
      "updateBy": "55b843a84df03bab3307c0fa",
      "ownerId": "55b843a84df03bab3307c0fa",
      "__v": 0,
      "allowUserApi": false,
      "manageByOpen": false
    }
  ]
}
```

<a name="Update Back Service"></a>
### Update Back Service

**Service Request**

> PUT https://api.oceanclouds.com/v1.0/developer/service/:backServiceId

Entity

| Entity key | description |
|:-|:-|
|name|Back service name.|
|signKey|A secure key for exchange message between app end user and back service. |
|messageApiAddress|Api address for receiving oceanclouds message.|
|serviceApiAddress|Api root address for app. |
|description| Description about this back service. |
|manageAddress|Your back service manage console address, this address should accept a appAuthCode to identify which app is visiting.|
|manageByOpen|True or False, Should this manage console open by a new window in ocean UI.|
|allowUserApi|True or False, is this back service a user auth back service?|

**Output**

Entity

Back Service Entity is 

| Entity key | description |
|:-|:-|
|_id|Back service id.|
|key|Back service key. Every back service have an individual key and it's unique in oceanclouds.|
|name|Back service name.|
|type|PRIVATE or PUBLIC. A PUBLIC back service can be subscribe by any app, PRIVATE back service can only used by owner app. For now user only can request a PRIVATE back service.|
|signKey|A secure key for exchange message between Oceanclouds and back service. |
|messageApiAddress|Api address for receiving oceanclouds message.|
|serviceApiAddress|Api root address for app. |
|description| Description about this back service. |
|createTime|Create time(Unix time millisecond) of this back service. |
|updateTime|Update time(Unix time millisecond) of this back service.|
|createBy|Create account ID.|
|updateBy|Update account ID.|
|ownerId|Owner account ID.|

API Error

|ErrorCode|Description|
|:-|:-|
|backService.doNotHaveRight|Do not have right to access this backService!|

**Sample**

PUT https://api.oceanclouds.com/v1.0/developer/service/55b8891c4df03bab3307c0fd
Input is 

```json
{
  "name": "TestService",
  "messageApiAddress":"https://localhost/api/message",
  "signKey":"sample_signKey",
  "serviceApiAddress": "https://localhost/api/service",
  "description":"This is a test back service.",
  "manageAddress":"https://localhost/console",
  "manageByOpen":false,
  "allowUserApi":false
}
```

Output is 

```json
{
  "success": true,
  "entity": {
    "_id": "55b8891c4df03bab3307c0fd",
    "name": "TestService",
    "key": "sample_test",
    "messageApiAddress": "https://localhost/api/message",
    "signKey": "sample_signKey",
    "serviceApiAddress": "https://localhost/api/service",
    "description": "This is a test back service.",
    "type": "PRIVATE",
    "manageAddress": "https://localhost/console",
    "createTime": 1438157084000,
    "updateTime": 1438157713000,
    "createBy": "55b843a84df03bab3307c0fa",
    "updateBy": "55b843a84df03bab3307c0fa",
    "ownerId": "55b843a84df03bab3307c0fa",
    "__v": 0,
    "allowUserApi": false,
    "manageByOpen": false
  }
}
```

<a name="Delete Back Service"></a>
### Delete Back Service

**Service Request**

> DELETE https://api.oceanclouds.com/v1.0/developer/service/:backServiceId

**Input**

Empty.

**Output**

No entity.

**Sample**

DELETE https://api.oceanclouds.com/v1.0/developer/service/55b8891c4df03bab3307c0fd
Input body is Empty.

Output body is

```json
{
  "success": true
}
```

<a name="App Manage"></a>
## App Manage

<a name="Create App"></a>
### Create App

**Service Request**

> POST https://api.oceanclouds.com/v1.0/developer/apps

**Input**

| Entity key | description |
|:-|:-|
|name|App name.|
|key|App key. Every app have an individual key and it's unique in oceanclouds.|

**Output**

Entity is

| Entity key | description |
|:-|:-|
|_id|App id.|
|name|App name.|
|key|App key. Every app have an individual key and it's unique in oceanclouds.|
|createTime|Create time(Unix time millisecond) of this back service. |
|updateTime|Update time(Unix time millisecond) of this back service.|
|createBy|Create account ID.|
|updateBy|Update account ID.|
|ownerId|Owner account ID.|

**Sample**

Input is

```json
{
  "name": "Test_App",
  "key": "test_app"
}
```
Output is 

```json
{
  "success": true,
  "entity": {
    "__v": 0,
    "name": "Test_App",
    "key": "test_app",
    "createTime": 1438158575000,
    "updateTime": 1438158575000,
    "createBy": "55b843a84df03bab3307c0fa",
    "updateBy": "55b843a84df03bab3307c0fa",
    "ownerId": "55b843a84df03bab3307c0fa",
    "_id": "55b88eef4df03bab3307c0ff"
  }
}

```

<a name="Read App"></a>
### Read App

**Service Request**

> GET https://api.oceanclouds.com/v1.0/developer/service/:appId

**Input**

Empty.

**Output**

Entities is 

| Entity key | description |
|:-|:-|
|_id|App id.|
|key|App key. Every app have an individual key and it's unique in oceanclouds.|
|name|App name.|
|createTime|Create time(Unix time millisecond) of this back service. |
|updateTime|Update time(Unix time millisecond) of this back service.|
|createBy|Create account ID.|
|updateBy|Update account ID.|
|ownerId|Owner account ID.|

**Sample**

GET https://api.oceanclouds.com/v1.0/developer/service/55b88eef4df03bab3307c0ff
Input is empty.

Output is 

```json
{
  "success": true,
  "entity": {
    "_id": "55b88eef4df03bab3307c0ff",
    "name": "Test_App",
    "key": "test_app",
    "createTime": 1438158575000,
    "updateTime": 1438158575000,
    "createBy": "55b843a84df03bab3307c0fa",
    "updateBy": "55b843a84df03bab3307c0fa",
    "ownerId": "55b843a84df03bab3307c0fa",
    "__v": 0
  }
}
```

<a name="Read Apps"></a>
### Read Apps

**Service Request**

> GET https://api.oceanclouds.com/v1.0/developer/apps

**Input**

Empty.

**Output**

Entities is array of 

| Entity key | description |
|:-|:-|
|_id|App id.|
|key|App key. Every app have an individual key and it's unique in oceanclouds.|
|name|App name.|
|createTime|Create time(Unix time millisecond) of this back service. |
|updateTime|Update time(Unix time millisecond) of this back service.|
|createBy|Create account ID.|
|updateBy|Update account ID.|
|ownerId|Owner account ID.|

**Sample**

Input is empty.

Output is 

```json
{
  "success": true,
  "rows": 1,
  "entities": [
    {
      "_id": "55b88eef4df03bab3307c0ff",
      "name": "Test_App",
      "key": "test_app",
      "createTime": 1438158575000,
      "updateTime": 1438158575000,
      "createBy": "55b843a84df03bab3307c0fa",
      "updateBy": "55b843a84df03bab3307c0fa",
      "ownerId": "55b843a84df03bab3307c0fa",
      "__v": 0
    }
  ]
}
```

<a name="Update App"></a>
### Update App

**Service Request**

> PUT https://api.oceanclouds.com/v1.0/developer/app/:appId

**Input**
| Entity key | description |
|:-|:-|
|name|App name.|

**Output**

Entity is

| Entity key | description |
|:-|:-|
|_id|App id.|
|name|App name.|
|key|App key. Every app have an individual key and it's unique in oceanclouds.|
|createTime|Create time(Unix time millisecond) of this back service. |
|updateTime|Update time(Unix time millisecond) of this back service.|
|createBy|Create account ID.|
|updateBy|Update account ID.|
|ownerId|Owner account ID.|

**Sample**

PUT https://api.oceanclouds.com/v1.0/developer/app/55b88eef4df03bab3307c0ff
Input is

```json
{
  "name": "TestApp1"
}
```
Output is 

```json
{
  "success": true,
  "entity": {
    "_id": "55b88eef4df03bab3307c0ff",
    "name": "TestApp1",
    "key": "test_app",
    "createTime": 1438158575000,
    "updateTime": 1438158575000,
    "createBy": "55b843a84df03bab3307c0fa",
    "updateBy": "55b843a84df03bab3307c0fa",
    "ownerId": "55b843a84df03bab3307c0fa",
    "__v": 0
  }
}

```

<a name="Delete App"></a>
### Delete App

**Service Request**

> DELETE https://api.oceanclouds.com/v1.0/developer/app/:appId

**Input**
Empty.

**Output**

No Entity.

**Sample**

DELETE https://api.oceanclouds.com/v1.0/developer/app/55b88eef4df03bab3307c0ff


Output is 

```json
{
  "success": true
}

```

<a name="Access Token"></a>
## Access Token

<a name="Get Access Tokens"></a>
### Get Access Tokens

**Service Request**

> GET https://api.oceanclouds.com/v1.0/developer/access_tokens

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
  "rows": 2,
  "entities": [
    {
      "_id": "55b886594df03bab3307c0fc",
      "accessTokenCode": "244697236045818dfd5cd62674d6266ad2183437",
      "type": "developer",
      "userAccountId": "55b843a84df03bab3307c0fa",
      "resourceKey": "test@oceanclouds.com",
      "resourceId": "55b843a84df03bab3307c0fa",
      "expireTime": 1438242777173,
      "__v": 0,
      "expired": false
    },
    {
      "_id": "55b88eef4df03bab3307c100",
      "accessTokenCode": "513f482368e5f01d9b3cdcea15c3839c7028312b",
      "type": "app",
      "userAccountId": "55b843a84df03bab3307c0fa",
      "resourceKey": "test_app",
      "resourceId": "55b88eef4df03bab3307c0ff",
      "expireTime": 1440750575173,
      "__v": 0,
      "expired": false
    }
  ]
}

```

<a name="Get Access Token"></a>
### Get Access Token

**Service Request**

> GET https://api.oceanclouds.com/v1.0/developer/access_token/:tokenType/:resourceId

- *TokenType include app,service,developer.*

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

GET https://api.oceanclouds.com/v1.0/developer/access_token/app/55b88eef4df03bab3307c0ff

Output is 

```json
{
  "success": true,
  "entity": {
    "_id": "55b88eef4df03bab3307c100",
    "accessTokenCode": "513f482368e5f01d9b3cdcea15c3839c7028312b",
    "type": "app",
    "userAccountId": "55b843a84df03bab3307c0fa",
    "resourceKey": "test_app",
    "resourceId": "55b88eef4df03bab3307c0ff",
    "expireTime": 1440750575173,
    "__v": 0,
    "expired": false
  }
}

```

<a name="Regenerate Access Token"></a>
### Regenerate Access Token

**Service Request**

> POST https://api.oceanclouds.com/v1.0/developer/access_token/:tokenType/:resourceId/regenerate

- *TokenType include app,service,developer.*

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

POST https://api.oceanclouds.com/v1.0/developer/access_token/app/55b88eef4df03bab3307c0ff/regenerate

Output is 

```json
{
  "success": true,
  "entity": {
    "__v": 0,
    "accessTokenCode": "d56578cabced07c5683bc964022d1a6f5fcd9a99",
    "type": "app",
    "userAccountId": "55b843a84df03bab3307c0fa",
    "resourceKey": "test_app",
    "resourceId": "55b88eef4df03bab3307c0ff",
    "expireTime": 1440751355191,
    "_id": "55b891fb4df03bab3307c101",
    "expired": false
  }
}

```