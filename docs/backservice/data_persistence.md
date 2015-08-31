#Data Persistence Service API 

Data persistence is a basic service for app to save their data. Normally, a app's business process is design to several CRUD data storage function.
This service provide app ability to design their own entities schema, and maintance the entity data via API.

Create or modify app's entity schema, please read the [Guide Doc](http://doc.oceanclouds.com/guide/en/index.html) of oceanclouds. 

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



##Create Entity Data

**Service Request**

> POST {ServiceApiRootAddress}/crud/:appKey/:entityName

**Input**

Json object of entity.

**Output**

Json object of already created entity.

**Sample**

Create data for entity blog(Which only have two business properties) .

Post to https://crud.service.oceanclouds.com/crud/sample_app/blog

Input header contains 

* Content-Type : application/json
* Ocean-Auth : 555831e56690866ef71c32583535cd8f620a5515fff7c4eca6a217af6c37672726f170e99c76bb951c404ce9e34cfb881bb60b8b971f5abb903ab903173dd1d5ebbd1f80c3a39f4667c875243fc13a70a64f1a6b3f8559ca18cb3649c9c42665908b4fa23690f6538f597f16af82583bdffa7ed237d38923e487f3fedea709de2f5dd137ae82c2779f83d5865b32f386

Input body is 

```json
{
	content: "Test blog content.",
	title: "This is test blog"
}
```
Output body is 

```json
{
  "success": true,
  "entity": {
    "__v": 0,
    "title": "This is test blog",
    "content": "Test blog content.",
    "createTime": 1425871050,
    "updateTime": 1425871050,
    "createBy": "changsure@weibo",
    "updateBy": "changsure@weibo",
    "_id": "54fd10ca8ed7344631a7e11b"
  }
}
```

##Read Entity Data

**Service Request**

> GET {ServiceApiRootAddress}/crud/:appKey/:entityName/:_id

**Input**

Empty.

**Output**

Json object of already created entity.

**Sample**

Read data for entity blog.

Get to https://crud.service.oceanclouds.com/crud/sample_app/blog/54fd10ca8ed7344631a7e11b

Input header contains 

* Content-Type : application/json
* Ocean-Auth : 555831e56690866ef71c32583535cd8f620a5515fff7c4eca6a217af6c37672726f170e99c76bb951c404ce9e34cfb881bb60b8b971f5abb903ab903173dd1d5ebbd1f80c3a39f4667c875243fc13a70a64f1a6b3f8559ca18cb3649c9c42665908b4fa23690f6538f597f16af82583bdffa7ed237d38923e487f3fedea709de2f5dd137ae82c2779f83d5865b32f386

Output body is 

```json
{
  "success": true,
  "entity": {
    "__v": 0,
    "title": "This is test blog",
    "content": "Test blog content.",
    "createTime": 1425871050,
    "updateTime": 1425871050,
    "createBy": "changsure@weibo",
    "updateBy": "changsure@weibo",
    "_id": "54fd10ca8ed7344631a7e11b"
  }
}
```

##Update Entity Data

**Service Request**

> PUT {ServiceApiRootAddress}/crud/:appKey/:entityName/:_id


**Input**

Json object of entity.

**Output**

Json object of already updated entity.

**Sample**

Update data for entity blog.

Put to https://crud.service.oceanclouds.com/crud/sample_app/blog

Input header contains 

* Content-Type : application/json
* Ocean-Auth : 555831e56690866ef71c32583535cd8f620a5515fff7c4eca6a217af6c37672726f170e99c76bb951c404ce9e34cfb881bb60b8b971f5abb903ab903173dd1d5ebbd1f80c3a39f4667c875243fc13a70a64f1a6b3f8559ca18cb3649c9c42665908b4fa23690f6538f597f16af82583bdffa7ed237d38923e487f3fedea709de2f5dd137ae82c2779f83d5865b32f386

Input body is 

```json
{
	content: "Test modify blog content.",
	title: "This is test blog(modify)"
}
```
Output body is 

```json
{
  "success": true,
  "entity": {
    "_id": "54fd10ca8ed7344631a7e11b",
    "title": "This is test blog(modify)",
    "content": "Test modify blog content.",
    "createTime": 1425871050,
    "updateTime": 1425871572,
    "createBy": "changsure@weibo",
    "updateBy": "changsure@weibo",
    "__v": 0
  }
}
```

##Delete Entity Data

**Service Request**

> DELETE {ServiceApiRootAddress}/crud/:appKey/:entityName/:_id

**Input**

Empty.

**Output**

Whether delete is sucess.

**Sample**

Delete data for entity blog.

Delete to https://crud.service.oceanclouds.com/crud/sample_app/blog/54fd10ca8ed7344631a7e11b

Input header contains 

* Content-Type : application/json
* Ocean-Auth : 555831e56690866ef71c32583535cd8f620a5515fff7c4eca6a217af6c37672726f170e99c76bb951c404ce9e34cfb881bb60b8b971f5abb903ab903173dd1d5ebbd1f80c3a39f4667c875243fc13a70a64f1a6b3f8559ca18cb3649c9c42665908b4fa23690f6538f597f16af82583bdffa7ed237d38923e487f3fedea709de2f5dd137ae82c2779f83d5865b32f386

Output body is 

```json
{
	"success":true
}
```

##Read All Entity Data

**Service Request**

> GET {ServiceApiRootAddress}/crud/:appKey/:entityName/find/query

**Input**

Empty.

**Output**

All entity data.

**Sample**

Read all data for entity blog.

Get to https://crud.service.oceanclouds.com/crud/sample_app/blog/find/query

Input header contains 

* Content-Type : application/json
* Ocean-Auth : 555831e56690866ef71c32583535cd8f620a5515fff7c4eca6a217af6c37672726f170e99c76bb951c404ce9e34cfb881bb60b8b971f5abb903ab903173dd1d5ebbd1f80c3a39f4667c875243fc13a70a64f1a6b3f8559ca18cb3649c9c42665908b4fa23690f6538f597f16af82583bdffa7ed237d38923e487f3fedea709de2f5dd137ae82c2779f83d5865b32f386

Output body is 

```json
{
  "success": true,
  "rows": 2,
  "entities": [
    {
      "_id": "54fd13898ed7344631a7e11c",
      "title": "Test1",
      "content": "Test1 content.",
      "createTime": 1425871753,
      "updateTime": 1425871753,
      "createBy": "changsure@weibo",
      "updateBy": "changsure@weibo",
      "__v": 0
    },
    {
      "_id": "54fd13928ed7344631a7e11d",
      "title": "Test2",
      "content": "Test2 content.",
      "createTime": 1425871762,
      "updateTime": 1425871762,
      "createBy": "changsure@weibo",
      "updateBy": "changsure@weibo",
      "__v": 0
    }
  ]
}
```

##Search Entity Data By Criteria

**Service Request**

> POST {ServiceApiRootAddress}/crud/:appKey/:entityName/find/query

**Input**

| key | description |
|:-|:-|
|criteria|Criteria about this query.|
|returnColumn|Properties that need to return.|
|rowDes|Row description, such as limit, skip, etc.|

**Output**

Empty.

**Sample**

Read criteria data for entity blog.

Post to https://crud.service.oceanclouds.com/crud/sample_app/blog/find/query

Input header contains 

* Content-Type : application/json
* Ocean-Auth : 555831e56690866ef71c32583535cd8f620a5515fff7c4eca6a217af6c37672726f170e99c76bb951c404ce9e34cfb881bb60b8b971f5abb903ab903173dd1d5ebbd1f80c3a39f4667c875243fc13a70a64f1a6b3f8559ca18cb3649c9c42665908b4fa23690f6538f597f16af82583bdffa7ed237d38923e487f3fedea709de2f5dd137ae82c2779f83d5865b32f386

Input body is 

```json
{
  "criteria": {
    "title": "Test1"
  },
  "returnColumn": "title content createTime",
  "rowDes": {
    "limit": 2
  }
}
```


Output body is 

```json
{
  "success": true,
  "rows": 1,
  "entities": [
    {
      "_id": "54fd13898ed7344631a7e11c",
      "title": "Test1",
      "content": "Test1 content.",
      "createTime": 1425871753
    }
  ]
}
```

## Error Codes


|ErrorCode|Description|
|:-|:-|
|common.unknow|Unknown error! Please contact our admin!|
|common.systemError|System get error.|
|common.database|Db error|
|common.404|Resource Not Found|
|common.messageTypeNotSupport|Message Type Not Support!|
|cache.canNotLoadEntitySchemaModelToCache|Entity schema format is not right.|
|entitySchema.entitySchemaNotFound|Can not find EntitySchema, please check your query.|
|entitySchema.entitySchemaAlreadyExist|EntitySchema already exist.|
|crud.entityNotFound|Can not find entity, please check your query.|
|crud.donNotHaveAppRight|Don't have right to access this APP manage.|
|crud.donNotHaveRight|Don't have right to access data object.|
|crud.notOwner|Not owner of this entity object.|
|ocean.notAuthorizeByOcean|Do not have Ocean-Auth Header, please check whether you already be authorize by Ocean.|
|subscribe.signNotCorrect|The signed is not correct, please check the sign key.|
|oauth.getAccessTokenFailed|Get access token from oceanclouds failed.|
|passport.notLogin|Not login,please login in oceanclouds.com first.|

