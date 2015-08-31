#Standard User API

Standard user service API provide user register, login, authorize and manage service for oceanclouds app. 

##Exchange Standard

Please fill these headers in your request.

**Request Header**

* Content-Type - application/json;charset=utf-8
* Ocean-Auth - Ocean-Auth is certificate which app client get from oceanclouds to prove this app user has the ability to visit back service api. Please get it from [Oceanclouds API Fetch App User Ocean Context](../ocean/api_for_application.md#Fetch App User Ocean Context)

**Request Body**

> Raw Json, based on the API demands.

**Request Method**

> POST, PUT, GET, DELETE

**Response Body**

The response Json Structure is 


```json
{
	"success": true,
	"entity":{
		"xxx":"xxx"
		...
	}
	"rows": 2,
	"entities":[{
			"xxx":"xxx"
			...
		}
		,{
			"xxx":"xxx"
			...
		}
	]
		
	"err": { 
		"name": "USER Error",
		"errCode": "user.alreadyExist",
		"errorMessage": "User account already exists!"
	}
}
```

The response Json Structure meaning is

|name|description|
|-:|:-|
|success|*true* or *false*.This value give you whether the request is successed. All error(system or business) will return an *false* value and the **err** property will show.|
|entity|An entity Object if the API return THE ENTITY such as update the entity by id. |
|rows|The entity number it returns. Only show when there is batch of entity returned.|
|entities|If the API return batch of entities, this property is used to store an array of entities.|
|err|If the **success** is *false*, err will show to contain an error description. | 
|err.name|The error name.|
|err.errCode|The error code.|
|err.errrorMessage|The error message Oceanclouds gives. You can change it based on the **err.errorCode**.|

## Register a User
This API will create a user for app.

**Service Request**

> POST {ServiceApiRootAddress}/register

**Input**

| key | description |
|:-|:-|
|accountName|App user account name|
|password|App user password|
|displayName|App user display name|
|email|App user email|
|cellphone|App user cellphone|


**Output**

Entity is 

| key | description |
|:-|:-|
|_id|App user id in user back service|
|accountName|App user account name|
|displayName|App user display name|
|email|App user email|
|cellphone|App user cellphone|
|appKey|Ocean app key|

**Sample**

Input is 

```json
{
	"accountName": "test",
	"password": "123456",
	"displayName":"Test User",
	"email": "test@test.com",
	"cellphone":"13512345678"
}
```

Output is 

```json
{
	"success": true,
	"entity": {
		"_id": "550bdcd82a1af669e5f4afe7",
		"accountName": "test",
		"displayName":"Test User",
		"email": "test@test.com",
		"cellphone":"13512345678",
		"appKey": "sample_app"
	}
}
```

## App user login 
This API will login by a user account and authorize an oceanclouds code for fetch ocean context.

**Service Request**

> POST {ServiceApiRootAddress}/login

**Input**

| key | description |
|:-|:-|
|accountName|App user account name|
|password|App user password|
|rememberMe|True or false. Yes for 30 days to expire, No for 1 day to expire.|

**Output**

Entity is 

| key | description |
|:-|:-|
|accessToken|Ocean access token for app end user |


**Sample**

Input is 

```json
{
	"accountName": "test",
	"password": "123456",
	"rememberMe":true
}
```

Output is 

```json
{
	"success": true,
	"entity": {
		"accessToken": "4f060b63a13eb14fdcd73a473a8a8e53f5b34bee"
	}
}
```

## App user update info
This API will update user information.

**Service Request**

> PUT {ServiceApiRootAddress}/update

**Input**

| key | description |
|:-|:-|
|accountName|App user account name|
|password|App user password|
|displayName|App user display name|
|email|App user email|
|cellphone|App user cellphone|


**Output**

Entity is 

| key | description |
|:-|:-|
|_id|App user id in user back service|
|accountName|App user account name|
|displayName|App user display name|
|email|App user email|
|cellphone|App user cellphone|
|appKey|Ocean app key|

**Sample**

Input is 

```json
{
	"accountName": "test",
	"password": "123456",
	"displayName":"Test User",
	"email": "test@test.com",
	"cellphone":"13512345678"
}
```

Output is 

```json
{
	"success": true,
	"entity": {
		"_id": "550bdcd82a1af669e5f4afe7",
		"accountName": "test",
		"displayName":"Test User",
		"email": "test@test.com",
		"cellphone":"13512345678",
		"appKey": "sample_app"
	}
}
```

## Error Code

|ErrorCode|Description|
|:-|:-|
|common.unknow|Unknown error! Please contact our admin!|
|common.systemError|System get error.|
|common.database|Db error|
|common.404|Resource Not Found|
|user.doNotHaveRight|Don't have right to update user!|
|user.alreadyExist|User account already exists!|
|user.accountOrPasswordNotRight|User account not exists or password not right!|
|user.notExist|User account not exists!|
|ocean.notAuthorizeByOcean|Do not have Ocean-Auth Header, please check whether you already be authorize by Ocean.|
|ocean.saveUserInfoFailed|Failed to save user info to oceanclouds.|
|subscribe.signNotCorrect|The signed is not correct, please check the sign key.|
|oauth.getAccessTokenFailed|Get access token from oceanclouds failed.|
|passport.notLogin|Not login, please login in oceanclouds.com first.|

