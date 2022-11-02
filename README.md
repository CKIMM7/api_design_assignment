***Consider the type of data we will be storing and therefore the type of database we should implement (SQL vs NoSQL)***

Data is already pre-defined and structured.
It is not expected to have unknow changes.
Therefore, I chose SQL

Each person has a name, age and number of people in their household
Each house has an address and an owner
Each address has a postcode and street address

***Create a schema for this database***

people table
    personId serial PRIMARY KEY,
    name VARCHAR(20) NOT NULL,
    age INT NOT NULL,
    householdsize INT NOT NULL,

households table
    householdId serial PRIMARY KEY,
    address VARCHAR(20) NOT NULL,
    owner INT NOT NULL,

people_households table
    personId int NOT NULL, 
    householdId int NOT NULL,
    FOREIGN KEY (personId) REFERENCES people(personId),
    FOREIGN KEY (householdId) REFERENCES households(householdId)


***Consider the requests our API should be capable of handling***
GET request

***List the routes you will need with their HTTP verb and path***

GET https://localhost/households

```
[
    {
      "householdId": 1,
      "address": [{"postcode" : "postcode1"}, {"streetaddress" : "streetaddress1"}],
      "owner": "personId"
    },
        {
      "householdId": 2,
      "address": [{"postcode" : "postcode2"}, {"streetaddress" : "streetaddress2"}],
      "owner": "personId"
    },
    ...
]
```

-householdId: unique identifer for this household
-address: address information for this household which contains a postcode and street address
-postcode: zip or postal code of this household
-streetaddress: street address of this household
-owner: owner of this household which is linked to personId


GET https://localhost/people

```
[
    {
      "personId": 1,
      "householdId": 1,
      "name": "Daniel",
      "age": 16,
      "householdMembers": 4,
    },
        {
      "personId": 2,
      "householdId": 2,
      "name": "John",
      "age": 57,
      "householdMembers": 15,
    },
    ...
]
```


-personId: unique identifer for this person
-householdId: unique identifer for this household
-name: name of this person
-age: age of this person
-householdMembers: number of household members that this person belongs to


GET https://localhost/households/{postcode}

```
[
    {
      "householdId": 1,
      "address": ["postCode1", "streetAddress1"],
      "owner": "personId"
    }
]
```

Parameters:
postcode (required): zip or postal code of the household being looked up


GET https://localhost/people/{name}

```
[
    {
      "personId": 1,
      "householdId": 1,
      "name": "Daniel",
      "age": 16,
      "householdMembers": 4,
    }
]
```

Parameters:
name (required): name of the person being looked up

GET https://localhost/people/?age={age}&householdmembers={size}

```
[
    {
      "personId": 12,
      "householdId": 7,
      "name": "Daniel",
      "age": 16,
      "householdMembers": 4,
    },
        {
      "personId": 22,
      "householdId": 13,
      "name": "Sarah",
      "age": 19,
      "householdMembers": 4,
    }
            {
      "personId": 37,
      "householdId": 22,
      "name": "Amy",
      "age": 17,
      "householdMembers": 4,
    }
    ...
]
```

Parameters:
age (required): age of the person being looked up to determine his/her age bracket
householdmembers (required): number of household members to determine the specific household size


***Determine the responses that should be returned and the content types of these requests and responses***

requests
Accepted Accept headers: application/json

responses
-When the api call works, you will see
Request Method: GET
Status Code: 200
Content-Type: application/json

-when a page or route is not found.
Request Method: GET
Status Code: 404
Content-Type: text/plain; charset=utf-8

-when the server is down
Request Method: GET
Status Code: 503 OK
Content-Type: text/plain; charset=utf-8












