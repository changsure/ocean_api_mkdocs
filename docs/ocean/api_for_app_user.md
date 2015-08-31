#Summary
This chapter show APIs that app client can use. 

* [Fetch Anonymous App User Ocean Context](#Fetch Anonymous App User Ocean Context)
* [Fetch Login App User Ocean Context](#Fetch Login App User Ocean Context)

<a name="Fetch Anonymous App User Ocean Context"></a>
## Fetch Anonymous App User Ocean Context

This call is **NOT** protected by access token, is a public API, but only for app end user to use.

**Service Request**

> POST https://api.oceanclouds.com/v1.0/public/ocean_context/:appKey

**Input**

Empty.

**Output**

Entity is

| key | description |
|:-|:-|
|userInfo.login|If the client login. If request with an authCode then this is *true*, if not this is *false*.|
|backServices|Hold an array of back service properties.|
|backServices.{backServiceKey}|Hold an entity of this back service.|
|backServices.{backServiceKey}.api|This back service api root address.|
|backServices.{backServiceKey}.oceanAuthHeader|This back service ocean auth header. When client request the back service api, this header is needed.|

API Error

|ErrorCode|Description|
|:-|:-|
|common.database|Db error|
|common.appKeyNotExists|Please check your input app key!|
|appUser.accessCodeNotExistsOrExpired|User Account access Code not exists or already expired, please login again to get new access code.|

**Sample**

GET https://api.oceanclouds.com/v1.0/public/ocean_context/sample_app


Output is 

```json
{
  "success": true,
  "entity": {
    "appKey": "sample_app",
    "userInfo": {
      "login": false
    },
    "backServices": {
      "crud": {
        "api": "https://crud.service.oceanclouds.com/crud",
        "oceanAuthHeader": "df16094d3ce6337a5e34eb8e866815e4962ea8cb882ccd3dda744d003f36042f5704b47a6961645f1ae1e8074621ae91"
      },
      "user": {
        "api": "https://user.service.oceanclouds.com/user",
        "oceanAuthHeader": "77d96db93349b3403ac4b98b367428df7e1271f9c3f7cbec74fcff3c9fe7c2205a1529fc1f4eb2032157db29c856fd10"
      },
      "weibo": {
        "api": "https://weibo.service.oceanclouds.com/wb",
        "oceanAuthHeader": "3534dd54111494de97822373ca1d3141a3cb5ac0ff67c8158170bb2b8211e7e58a69d09297abd1b254b5612b2e9ad3de"
      },
      "facebook": {
        "api": "https://fb.service.oceanclouds.com/fb",
        "oceanAuthHeader": "c0b17ed24f7c5030162871866795e8336559cc6c8b39cd31e54f34ef3eea0866fbeb9a5b82624ca0451553a69da1806a"
      }
    }
  }
}

```


<a name="Fetch Login App User Ocean Context"></a>
## Fetch Login App User Ocean Context

This API is protected by app end user access token, make sure get it from auth back service, then fill it in to AccessToken header to call this API.

**Service Request**

> POST https://api.oceanclouds.com/v1.0/end/ocean_context/:appKey

**Input**

Empty.

**Output**

Entity is

| key | description |
|:-|:-|
|userInfo.login|If the client login. If request with an authCode then this is *true*, if not this is *false*.|
|backServices|Hold an array of back service properties.|
|backServices.{backServiceKey}|Hold an entity of this back service.|
|backServices.{backServiceKey}.api|This back service api root address.|
|backServices.{backServiceKey}.oceanAuthHeader|This back service ocean auth header. When client request the back service api, this header is needed to identify which app user this client stand for.|

API Error

|ErrorCode|Description|
|:-|:-|
|common.database|Db error|
|common.appKeyNotExists|Please check your input app key!|


**Sample**

POST https://api.oceanclouds.com/v1.0/end/ocean_context/sample_app

Output is

```json
{
  "success": true,
  "entity": {
    "expireTime": 1440753398107,
    "appKey": "sample_app",
    "userInfo": {
      "login": true,
      "accountId": "55b750bf4se03bab3307c0e5",
      "accountName": "test",
      "authBackServiceKey": "user",
      "name": "test"
    },
    "backServices": {
      "crud": {
        "api": "https://crud.service.oceanclouds.com/crud",
        "oceanAuthHeader": "df16094d3ce6337a5e34eb8e866815e4962ea8cb882ccd3dda744d003f36042fe70185651132ba483a948b5c2c84ff2db2d9666953a0f5a10f69ee40ee3af3bd8f94e6d99bc7fe0994e816946f85480ec6f9db87ee378d04e57c57a8cd3bc2fbe974cb6fbaa810db3fbf781c95cbbdac49758a7adb4337b6a37a71eb6cdb0545564fc0b2366e60aa040a7b2d1cf1cff9cc59670dfed742ac8af1fb4bffa5148db6a38e06c7f18139cf31ab365da3c4ea082f0dd612ed5b0d40cebb41db04a3df961ba667cb08b57d91e565de9c7d997b"
      },
      "user": {
        "api": "https://user.service.oceanclouds.com/user",
        "oceanAuthHeader": "77d96db93349b3403ac4b98b367428df7e1271f9c3f7cbec74fcff3c9fe7c220d3f66d3d02a52fb3ca7ed8d477c219933c459195de7678ae2194afea7dsfsdsdacab4ac97c837c3157f719799d79891f0a2cea64557027444716198c5bfe8906942167d921da3fac3bca8f4ab918c12b007d70e81d424baae5177bf7b40760a6a1c91ce3474ff36e59bcb48805e3a0ecc75aa37791f9db145c544a57dcb778f66c9cd099a517a728425ca0e07627daafa6c427f90568376a4b552b9613369c69d2a214c209ebcbc6053aafa9ea58b3b897"
      },
      "weibo": {
        "api": "https://weibo.service.oceanclouds.com/wb",
        "oceanAuthHeader": "3534dd54111494de97822373ca1d3141a3cb5ac0ff67c8158170bb2b8211e7e55e226897fb32d351d623a7766e0e4f35ec3435d9eb5bbc3c1365070ef5a01c40aa840a7d257f6e4e4116282885599962d0cb2c5a1d12fbe7c81eb600e4c399af7a19aabd73ccd81e4e0werewrb1f3134254292abe47c33ea9bdd2e2d6362ba1a13d25ede02b91445120616a0c5e4c81c0e024e31f9619cbfd48ea733412ee0851516d643b5e1455a4682a284cc3b29373328f9344b6911262e95756e9ef419328664777c2665ae2de86291b391e3350cfff"
      },
      "facebook": {
        "api": "https://fb.service.oceanclouds.com/fb",
        "oceanAuthHeader": "c0b17ed24f7c5030162871866795e8336559cc6c8b39cd31e54f34ef3eea08663196e0ef3c2c96c6480f82983be5f9525a7c0662487d04fc9c1ererewrwewrerea8c0977dde090fd20162d0216f843a90430efa964ca225766ae1a2d12f2ecd0a7e5f9ab1b4e281075fba957403e09578725303ac19a9be864d2350381d431418ce67875221145a313e5f702893ce030c1a92452c895a09c1941e6a214e3567714"
      }
    }
  }
}
```
