#Facebook User Service API 

Facebook user service provide facebook user authorize service.

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
		"name": "Ocean Error",
		"errCode": "passport.loginFailed",
		"errorMessage": "User accountName or password not right!"
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

##Login By Facebook Account Code

This api will use facebook OAuth code to authorize, and return a Oceanclouds app user code.

**Service Request**

> GET {ServiceApiRootAddress}/wb/authwb/:appKey/auth?code={facebookAccoutAuthCode}


**Input**

* FacebookAccoutAuthCode - This value is returned by facebook OAuth callback. Detail infomation please visit [facebook api](https://developers.facebook.com/docs/facebook-login/manually-build-a-login-flow/v2.3).

**Output**

| key | description |
|:-|:-|
|accessToken|Ocean access token for app end user. More information please visit [Oceanclouds API Fetch App User Ocean Context](../ocean/api_for_app_user.md)|

**Sample**

Get to https://fb.service.oceanclouds.com/wb/authwb/sample_app/auth?code=c7af1e39de508c7f64795ca2f787e6cb

Output body is 

```json
{
  "success": true,
  "entity": {
    "accessToken": "9ca1fa7abac4ed9ffd9435e56f5d1103e07a4aa8"
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
|facebook.accessFailed|Access to facebook failed!|
|facebook.infoFailed|Get user info from facebook failed!|
|ocean.notAuthorizeByOcean|Do not have Ocean-Auth Header, please check whether you already be authorize by Ocean.|
|ocean.saveUserInfoFailed|Failed to save user info to oceanclouds.|
|subscribe.signNotCorrect|The signed is not correct, please check the sign key.|
|oauth.getAccessTokenFailed|Get access token from oceanclouds failed.|
|passport.notLogin|Not login, please login in oceanclouds.com first.|
