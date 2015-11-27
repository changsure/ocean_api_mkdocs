#Standard User API

Standard user service API provide user register, login, authorize and manage service for oceanclouds app. 

##Exchange Standard

Please fill these headers in your request.

**Request Address**
For any end user, the back service address is fetched by [Oceanclouds API Fetch App User Ocean Context](../ocean/api_for_app_user.md#Fetch App User Ocean Context) .  {ServiceApiRootAddress} will stand for the address from the context in this document. Fow now Stardard User API is using https://user.service.oceanclouds.com/user, but we strongly recommand your app to use the address from ocean context in case we change the address.


**Request Header**

* Content-Type - application/json;charset=utf-8
* Ocean-Auth - Ocean-Auth is certificate which app client get from oceanclouds to prove this app user has the ability to visit back service api. Please get it from [Oceanclouds API Fetch App User Ocean Context](../ocean/api_for_app_user.md#Fetch App User Ocean Context)

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


## App user update password
This API will update user password.

**Service Request**

> PUT {ServiceApiRootAddress}/update_password

**Input**

| key | description |
|:-|:-|
|oldPassword|Current password of the end user|
|newPassword|New password of the end user|

**Output**

Success or Error.

**Sample**

Input is 

```json
{
  "oldPassword":"123456",
  "newPassword":"654321"
}
```

Output is 

```json
{
	"success": true
}
```

## App user forget password
This API will send a reset password email to end user's email address. 

**Service Request**

> POST {ServiceApiRootAddress}/forget_password

**Input**

End user can choose use accountName or accountEmail to identify his account.

| key | description |
|:-|:-|
|accountName|The account name|
|accountEmail|The account email|

**Output**

Success or Error.

**Sample**

Input is 

```json
{
  "accountName":"testaccount"
}
```

or

```json
{
  "accountEmail":"test@testdomain.com"
}
```

Output is 

```json
{
	"success": true
}
```

## App user reset password
This API will reset user password by user reset password token. This token is send to user's email address from the forget password api.

**Service Request**

> PUT {ServiceApiRootAddress}/reset_password

**Input**

| key | description |
|:-|:-|
|resetToken|The reset token from the reset email|
|newPassword|New password of the end user|

**Output**

Success or Error.

**Sample**

Input is 

```json
{
  "resetToken":"4ffe0ed2683dc22aff02e2a14f8a9b79d09978a9",
  "newPassword":"123456"
}
```

Output is 

```json
{
	"success": true
}
```


## Error Code

|ErrorCode|Description|
|:-|:-|
|common.unknow|Unknown error! Please contact our admin!|
|common.database|Db error|
|common.404|Resource Not Found|
|mail.failed|Send mail failed|
|mail.reset.maxNumPerDay|Reset password mail send time touch max number!|
|token.notExist|Reset token not exist!|
|token.expired|Reset token already expired!|
|token.used|Reset token already used!|
|app.notSubscribedApp|This app do not subscribe user service, please check in ocean clouds console!|
|app.mailAlreadyEnabled|Current resource not supported when mail is enabled!|
|user.doNotHaveRight|Don't have right to update user!|
|user.alreadyExist|User account already exists!|
|user.accountOrPasswordNotRight|User account not exists or password not right!|
|user.passwordNotRight|Password not right!|
|user.notExist|User account not exists!|
|user.accountOrEmailCannotBeNull|User account or user email must filled!|
|ocean.notAuthorizeByOcean|Do not have Ocean-Auth Header, please check whether you alreb||uthorize by Ocean.|
|ocean.wrongOceanAuthBackServiceKey|Your ocean auth back service key is not right.|
|ocean.saveUserInfoFailed|Failed to save user info to oceanclouds.|
|ocean.getEndUserAccessTokenFailed|Failed to get app user access token from oceanclouds.|
|subscribe.signNotCorrect|The signed is not correct, please check the sign key.|
|auth.getAccessTokenFailed|Get access token from oceanclouds failed.|
|passport.notLogin|Not login,please login in oceanclouds.com first.|
|request.oceanMessageFail|Visit Ocean Message Api failed!|
|common.systemError|System get error|

