This is a handbook of describing the details of oceanclouds APIs and official back service APIs.

# Catalog

* OceanClouds API
	* [OceanClouds API for Public](ocean/api_for_public.md)
	* [OceanClouds API for Developer](ocean/api_for_developer.md)
	* [OceanClouds API for backservice](ocean/api_for_backservice.md)
	* [OceanClouds API for Application](ocean/api_for_application.md)
	* [OceanClouds API for App User](ocean/api_for_app_user.md)
* Official BackService API
	* [Standard User API](backservice/standard_user.md)
	* [Data Persistence API](backservice/data_persistence.md)
	* [Weibo User API](backservice/weibo_user.md)
	* [Facebook User API](backservice/facebook_user.md)


Oceanclouds system provides series of apis for it's self , for back service system and for app client.


## Ocean API Structure

**Request Header**

* Content-Type - application/json;charset=utf-8
* AccessToken - Access token is certificate which your identity to visit resource. It has four types, **developer, app, service, end** . Our api zone is protect by different access token type, such as if you are calling API for developer, then you need to fill a developer access token code in this header. 

When request protected ocean API, systen required access token to visit resources. There are:

1. Developer Access Token 
1. App Access Token
1. Back Service Access Token
1. End User Access Token

These api can get you access token 

- [Login](ocean/api_for_public.md#Login)
- [Get Access Tokens](ocean/api_for_developer.md#Get Access Tokens)
- [Get Access Token](ocean/api_for_developer.md#Get Access Token)


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


## Full Error Codes For Ocean API


|ErrorCode|Description|
|:-|:-|
|common.database|Db error|
|common.database.dataNotFound|Can not found data please check your request data param!|
|common.database.dataCanNotAccessed|Can not access data current user don't have this data access permission!|
|common.systemError|System get error.|
|common.404|Resource Not Found|
|common.appKeyNotExists|Please check your input app key!|
|common.backServiceKeyNotExists|Please check your input back service key!|
|accessToken.NotEmpty|Please fill your accessToken in request header!|
|accessToken.NotExist|Access token not exist!|
|accessToken.Expired|Access token already expired!|
|accessToken.TypeNotRight|You may use the wrong access token type to access resource!|
|accessToken.WrongTokenType|Your token type is wrong!|
|authCode.NotExist|Auth code not exist!|
|authCode.Expired|Auth code already expired!|
|authCode.TypeNotRight|You may use the wrong auth code type to access resource!|
|passport.emailAlreadyExist|User email is already used by another account!|
|passport.invitationNotRight|Your invitation code can not be found or already be used!|
|passport.emailFormatNotRight|User account email format is not right!|
|passport.cellPhoneFormatNotRight|User account cellphone format is not right!|
|passport.loginFailed|User accountName or password not right!|
|passport.noAccount|User account can not be found!!|
|backService.doNotHaveRight|Do not have right to access this backService!|
|backService.noSubscribeRecordFound|No subscription record found for app.|
|app.doNotHaveRight|Do not have right to access this app!|
|app.canNotDeleteBecauseUnCancelledSubscription|Can not delete application because some subscription is still on this app please cancel them first!|
|app.appAlreadySubscribeThisBackService|App already subscribe this back service!|
|app.appNotHaveThisBackService|App don not have this back service!|
|app.canNotCancelBackServiceBecauseOfWrongStatus|App can not cancel back service because the status is not for cancelling!|
|app.subscribeBackServiceNotExist|Subscribing service id not exist!|
|app.subscribeBackServiceIsPrivate|Private back service can only subscribed by owner app!|
|appUser.userNotFoundByAccessToken|User Account can not be found by access token please contact our admin.|
|message.notSupportEntityType|Not support entity type!|
|message.notSupportMessageType|Not support message type!|
|message.messageSendFailed|Visit back service message address failed!|
|common.unknown|Unknown error! Please contact our adm









