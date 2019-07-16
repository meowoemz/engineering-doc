## Pardot

### Authentication
Every api call in pardot need pardot user request an ```api_key```

```POST https://pi.pardot.com/api/login/version/3```

Parameter | Required | Description
--------- | -------- | -----------
```email```|    X    | The email address of your user account
```password```| X    | The password of your user account
```user_key```| X    | The 32-bit hexadecimal user key for your user account

**Sample Response**
```xml
<?xml version="1.0" encoding="UTF-8"?>
<rsp stat="ok" version="1.0">
    <api_key>xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx</api_key>
    <version>4</version>
</rsp>
```

You could get your api_key and version, and you need to call corresponding version of api.

Visit following url to get full documentation of Pardot api:
http://developer.pardot.com/

## SalesForce

**HEADER Required**

*`Post`*
 
```Authorization:Bearer AUTH_TOKEN && Content-Type:application/json```

*`GET`*

`Authorization:Bearer AUTH_TOKEN`
### Auth
**1. Auth Token**

Every api call require an `Auth_token`

**Request URL**
```
POST https://login.salesforce.com/services/oauth2/token
```
**Request Data**

Parameter | Description
--------- | -----------
`grant_type` | password
`client_id` | Consumer Key
`client_secret` | Consumer Secret
`username` | salesforce login username
`password` | salesforce login password

**Sample Response**
```
{"id":
    "https://login.salesforce.com/id/00Dx0000000BV7z/005x00000012Q9P",
"issued_at":
    "1278448832702","instance_url":"https://yourInstance.salesforce.com/",
"signature":
    "0CmxinZir53Yex7nE0TD+zMpvIWYGb/bdJh6XfOH6EQ=",
"access_token":
    "00Dx0000000BV7z!AR8AQAxo9UfVkh8AlV0Gomt9Czx9LjHnSSpwBMmbRcgKFmxOtvxjTrKW1
    9ye6PE3Ds1eQz3z8jr3W7_VbWmEu4Q8TVGSTHxs"}
```

### Contact
**1. Get Contact**

**Request URL**
```
GET https://na30.salesforce.com/services/data/v31.0/search/?q=Encoded SOSL search string
```
**Prepare SOSL Search String**

`-Before encode`

```
FIND {chengnanzhao123@gmail.com} IN ALL FIELDS RETURNING Contact
```

`-After encode`

```
FIND%20%7Bchengnanzhao123%40gmail.com%7D%20IN%20ALL%20FIELDS%20RETURNING%20Contact
```
use following website to encode SOSL search string

http://meyerweb.com/eric/tools/dencoder/

**Sample Response**

```
[
  {
    "attributes": {
      "type": "Contact",
      "url": "/services/data/v31.0/sobjects/Contact/0033600000mzjvRAAQ"
    },
    "Id": "0033600000mzjvRAAQ"
  }
]
```
### Search Record
**1. Create Search Record**

**Request URL**
```
POST https://na30.salesforce.com/services/data/v31.0/sobjects/SearchRecord__c
```
**Prepare Request Data**

`Request data must be in JSON format`
```
{
  "contactId__c": "0033600000mzjvRAAQ",
  "criteria__c":"this is another test" (can't be null)
}
```
**Sample Response**

```
{
  "id": "a5n36000000H1O2AAK",
  "success": true,
  "errors": []
}
```

References:

https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/resources_search.htm

https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/intro_understanding_username_password_oauth_flow.htm




