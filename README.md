***Consider the type of data we will be storing and therefore the type of database we should implement (SQL vs NoSQL)***

Data is already pre-defined and structured.
It is not expected to have unknow changes.
Therefore, I decided to use SQL.

***Create a schema for this database***

people table <br />
    personId serial PRIMARY KEY,<br />
    name VARCHAR(20) NOT NULL,<br />
    age INT NOT NULL,<br />
    householdsize INT NOT NULL,<br />

households table
    householdId serial PRIMARY KEY,<br />
    address VARCHAR(20) NOT NULL,<br />
    owner INT NOT NULL,<br />

people_households table <br />
    personId int NOT NULL, <br />
    householdId int NOT NULL,<br />
    FOREIGN KEY (personId) REFERENCES people(personId),<br />
    FOREIGN KEY (householdId) REFERENCES households(householdId)<br />


***Consider the requests our API should be capable of handling***
GET request

***List the routes you will need with their HTTP verb and path***

GET https://neighboursearch/households

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


GET https://neighboursearch/people

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


GET https://neighboursearch/households/{postcode}

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


GET https://neighboursearch/people/{name}

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

GET https://neighboursearch/people/?age={age}&householdmembers={size}

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
-When the api call works, you will see<br />
Request Method: GET<br />
Status Code: 200<br />
Content-Type: application/json<br />

-when a page or route is not found.<br />
Request Method: GET<br />
Status Code: 404<br />
Content-Type: text/plain; charset=utf-8<br />

-when the server is down<br />
Request Method: GET<br />
Status Code: 503 OK<br />
Content-Type: text/plain; charset=utf-8<br />












