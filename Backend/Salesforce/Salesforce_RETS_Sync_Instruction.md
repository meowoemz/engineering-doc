# Prerequisites

1. `PHRETS` package

For `Laravel`: 
```
"require": {
    "troydavisson/phrets": "2.*"
}
```

_Reference doc_: 

https://github.com/troydavisson/PHRETS

2. `PHEANSTALK` package
```
"require": {
    "pda/pheanstalk": "~3.0"
}
```

_Reference doc_:

https://github.com/pda/pheanstalk

3. RETS credentials(name format might be different)
```
username:
password:
login_url:
api_base:
```

4. Salesforce credential
```
SALESFORCE_TOKEN:
SALESFORCE_INSTANCE_URL
```

# Sync Process

## Pull data from RETS
1. Import `PHRETS`
```
use PHRETS\Configuration;
use PHRETS\Session;
```

2. Create `config` instance
```
$config = Configuration::load([
            'login_url' => env('RETS_LOGIN_URL'),
            'username' => env('RETS_ACCOUNT'),
            'password' => env('RETS_PASSWORD'),
            'rets_version' =>env('RETS_VERSION')(optional),
            'user_agent' =>env('RETS_USER_AGENT')(optional),
            'http_authentication'=>env('RETS_HTTP_AUTHENTICATION')(optional)
        ]);
```

3. start session and login
```
$rets = new Session($config);
$bulletin = $rets->Login();
```
implement singleton to avoid duplicate login problem

4. perform search
```
$result = $rets->Search('Property', $keyWord, $query);
```
`$keyWord`

`https://retsmd.com/`
use your rets credential to login, you can find available values in `Property` section.

`$query`

for this part, you need to prepare your query using `DMQL2`, which has specific syntax

http://www.exacthelp.com/2012/01/dmql-tutorial.html

https://www.flexmls.com/developers/rets/tutorials/dmql-tutorial/



Sample response
```
TODO
```

## Mapping RETS data to Salesforce
```
$salesforce_data = [
            'Name' => $listing_name,
            'pba__Area_pb__c' => $mred_data['AR'],
            'pba__TotalArea_pb__c' => $mred_data['ASF'],
            'pba__Bedrooms_pb__c' => $mred_data['BRALL'],
            'pba__FullBathrooms_pb__c' => $mred_data['BTH'],
            'pba__City_pb__c' => $mred_data['CIT'],
            'pba__HalfBathrooms_pb__c' => $mred_data['HALF_BATHS'],
            'pba__Address_pb__c' => $mred_data['HSN'] . ' ' . $mred_data['STR'],
            'pba__Listing_Agent_Mobil_Phone__c' => $mred_data['LACELLPHONE'],
            'pba__Listing_Agent_City__c' => $mred_data['LACITY'],
            'pba__Listing_Agent_Firstname__c' => $mred_data['LAFIRSTNAME'],
            'pba__Listing_Agent_Lastname__c' => $mred_data['LALASTNAME'],
            'pba__Listing_Agent_Phone__c' => $mred_data['LAOFFICEPHONE'],
            'pba__Latitude_pb__c' => $mred_data['LAT'],
            'Listed_Date__c' => $mred_data['LD'],
            'pba__ListingType__c' => $mred_data['LIST'],
            'MLS_ID__c' => $mred_data['LN'],
            'pba__Longitude_pb__c' => $mred_data['LNG'],
            'ParkingSpaces__c' => $mred_data['NO_PARKING_SPACES'],
            'pba__Description_pb__c' => $mred_data['REMARKS'],
            'pba__Status__c' => $mred_data['ST'],
            'State__c' => $mred_data['STATE'],
            'pba__Listing_Website__c' => $mred_data['TOURURL'],
            'pba__PostalCode_pb__c' => $mred_data['ZP']
        ];
```