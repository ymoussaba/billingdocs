# Wizall Payment Gateway

GETTING STARTED
----
Every request to **testfactures.wizall.com** must have an *authorization* field in header with value ``Token xxxxxxxxxxx``

Token can be obtained by making a POST request to **factures.wizall.com/token/** with parameters *username* and *password* in JSON format like this :

``` 
wget --quiet \
  --method POST \
  --header 'content-type: application/json' \
  --body-data '{"username": "USERNAME","password": "PASSWORD"}' \
  --output-document \
  - https://factures.wizall.com/token/
```

SENELEC
----
request related to SENELEC services

### Bills list
Returns json array of bill for a policy number

- **URL:** /senelecfactures/{policy_number}/
- **Method:** ``GET``
- **URL Params:** None
- **Data Params:** None
- **Success Response:**
	- **Code:** 200
	- **Content:**

```
[
    {
        "PAYMENT_TRANSACTION_NUMBER": null,
        "police": "1061103482",
        "numfacture": "5589110",
        "client": "CISSE BABACAR       ",
        "montant": "18590",
        "dateecheance": "2017-08-05",
        "statuspayment": false
    }
]
```
- **Error Response:**
	- **Code:** 401
	- **Content:** ```{ "detail": "Authentication credentials were not provided." }```

	
- **Sample Call:**

```
wget --quiet \
  --method GET \
  --header 'authorization: Token YOUR_TOKEN' \
  --output-document \
  - https://factures.wizall.com/senelecfactures/1061103482
```

### Pay bill
Returns paid bill as json object

- **URL:** /senelecfactures/
- **Method:** ``POST``
- **URL Params:** None
- **Data Params:** None
	- `msisdn`
	- `police`
  	- `numfacture`
  	- `montant`
  	- `pincode`
- **Success Response:**
	- **Code:** 200
	- **Content:**

```
{
    "PAYMENT_TRANSACTION_NUMBER": "55354a218",
    "police": "1061103482",
    "numfacture": "5589110",
    "client": "CISSE BABACAR",
    "montant": "18590",
    "dateecheance": "2017-08-05",
    "statuspayment": true
}
```

- **Error Response:**
	- **Code:** 400
	- **Content:** ``{ "code": "400", "error": "BILL_ALREADY_PAID" }``
	
	***OR***
	
	- **Code:** 401
	- **Content:** ``{ "detail": "Authentication credentials were not provided." }``
	
- **Sample Call:**

```
wget --quiet \
  --method POST \
  --header 'authorization: Token YOUR_TOKEN' \
  --header 'content-type: application/json' \
  --body-data '{"msisdn":"771234567","police": 	"1061103482","numfacture": "5589110","montant":	"18590","pincode":"1234"}' \
  --output-document \
  - https://factures.wizall.com/senelecfactures/
```

### User policies list
Returns json array of user saved policies

- **URL:** /senelecpolice/{phone_number}/
- **Method:** ``GET``
- **URL Params:** None
- **Data Params:** None
- **Success Response:**
	- **Code:** 200
	- **Content:**

```
[
    {
        "id": 29,
        "alias": "Sweet Home",
        "msisdn": 771234567,
        "police": "106A250566"
    },
    {
        "id": 30,
        "alias": "Test",
        "msisdn": 771234567,
        "police": "1101107740"
    }
]
```
	
- **Sample Call:**

```
wget --quiet \
  --method GET \
  --header 'authorization: Token YOUR_TOKEN' \
  --output-document \
  - https://factures.wizall.com/senelecpolice/7711661821/
```

- **Error Response:**
	- **Code:** 401
	- **Content:** ``{ "detail": "Authentication credentials were not provided." }``

### Add policy number to user collection
Returns added policy details as json object

- **URL:** /senelecpolice/
- **Method:** ``POST``
- **URL Params:** None
- **Data Params:** 
	- `alias`
	- `msisdn`
	- `police`
- **Success Response:**
	- **Code:** 200
	- **Content:**

```
{
    "id": 67,
    "alias": "Hotel",
    "msisdn": 771234567,
    "police": "4109900642"
}
```
	
- **Sample Call:**

```
wget --quiet \
  --method POST \
  --header 'authorization: Token YOUR_TOKEN' \
  --header 'content-type: application/json' \
  --body-data '{"alias":"Hotel", "msisdn":"771166182", "police":"4109900642"}' \
  --output-document \
  - https://factures.wizall.com/senelecpolice/
```
- **Error Response:**
	- **Code:** 404
	- **Message:** 404 Not Found

	
### Delete policy number from user collection

- **URL:** /deletepolice/ID_NUMBER/
- **Method:** ``DELETE``
- **URL Params:** None
- **Data Params:** None
- **Success Response:**
	- **Code:** 200
	- **Content:** None
- **Error Response:**
	- **Code:** 404
	- **Message:** 404 Not Found

- **Sample Call:**

```
wget --quiet \
  --method DELETE \
  --header 'authorization: Token YOUR_TOKEN' \
  --output-document \
  - https://factures.wizall.com/deletepolice/67/
```


SDE
----

### Bills list
Returns json array of bill for a reference number

- **URL:** /sde/{reference_number}/
- **Method:** ``GET``
- **URL Params:** None
- **Data Params:** None
- **Success Response:**
	- **Code:** 200
	- **Content:**

```
[
    {
        "PAYMENT_TRANSACTION_NUMBER": null,
        "reference_client": "735034654215",
        "reference_facture": "10073503465421502051701",
        "nom": "M.SALIOU",
        "prenom": "DIEYE",
        "montant": "2828",
        "date_echeance": "15/06/2017",
        "statuspayment": false
    }
]
```
- **Error Response:**
	- **Code:** 401
	- **Content:** ```{ "detail": "Authentication credentials were not provided." }```

	
- **Sample Call:**

```
wget --quiet \
  --method GET \
  --header 'authorization: Token YOUR_TOKEN' \
  --output-document \
  - https://factures.wizall.com/sde/735034654215/
```

### Pay bill
Returns paid bill as json object

- **URL:** /sde/
- **Method:** ``POST``
- **URL Params:** None
- **Data Params:** None
	- `msisdn`
	- `reference_client`
  	- `reference_facture`
  	- `montant`
  	- `pincode`
- **Success Response:**
	- **Code:** 200
	- **Content:**

```
{
    "PAYMENT_TRANSACTION_NUMBER": "029a67f9f",
    "reference_client": "735034654215",
    "reference_facture": "10073503465421502051701",
    "nom": "M.SALIOU",
    "prenom": "DIEYE",
    "montant": "2828",
    "date_echeance": "15/06/2017",
    "statuspayment": true
}
```

- **Error Response:**
	- **Code:** 400
	- **Content:** ``{ "code": "400", "error": "BILL_ALREADY_PAID" }``
	
	***OR***
	
	- **Code:** 401
	- **Content:** ``{ "detail": "Authentication credentials were not provided." }``
	
- **Sample Call:**

```
wget --quiet \
  --method POST \
  --header 'authorization: Token YOUR_TOKEN' \
  --header 'content-type: application/json' \
  --body-data '{ "reference_client":"735034654215", "reference_facture":"10073503465421502051701", "montant":"2828",  "pincode":"1001", "msisdn":"771234567"}' \
  --output-document \
  - https://factures.wizall.com/sde/
```

### User references list
Returns json array of user saved references

- **URL:** /sdereference/{phone_number}/
- **Method:** ``GET``
- **URL Params:** None
- **Data Params:** None
- **Success Response:**
	- **Code:** 200
	- **Content:**

```
[
    {
        "id": 29,
        "alias": "Sweet Home",
        "msisdn": 771234567,
        "police": "106A250566"
    },
    {
        "id": 30,
        "alias": "Test",
        "msisdn": 771234567,
        "police": "1101107740"
    }
]
```
- **Error Response:**
	- **Code:** 401
	- **Content:** ``{ "detail": "Authentication credentials were not provided." }``

- **Sample Call:**

```
wget --quiet \
  --method GET \
  --header 'authorization: Token YOUR_TOKEN' \
  --output-document \
  - https://factures.wizall.com/sdereference/771234567
```

### Add reference number to user collection
Returns added reference details as json object

- **URL:** /sdereference/
- **Method:** ``POST``
- **URL Params:** None
- **Data Params:**
	- `alias`
	- `msisdn`
	- `reference`
- **Success Response:**
	- **Code:** 200
	- **Content:**

```
{
    "id": 52,
    "alias": "Chateau Ngor",
    "msisdn": 771234567,
    "reference": 735034938607
}
```
	
- **Sample Call:**

```
wget --quiet \
  --method POST \
  --header 'authorization: Token YOUR_TOKEN' \
  --header 'content-type: application/json' \
  --body-data '{"alias":"Chateau Ngor", "msisdn":"771234567", "reference":"735034938607"}' \
  --output-document \
  - https://factures.wizall.com/sdereference/
```
- **Error Response:**
	- **Code:** 404
	- **Message:** 404 Not Found


### Delete reference number from user collection

- **URL:** /deleteref/ID_NUMBER/
- **Method:** ``DELETE``
- **URL Params:** None
- **Data Params:** None
- **Success Response:**
	- **Code:** 200
	- **Content:** None
- **Error Response:**
	- **Code:** 404
	- **Message:** 404 Not Found

- **Sample Call:**

```
wget --quiet \
  --method DELETE \
  --header 'authorization: Token YOUR_TOKEN' \
  --output-document \
  - https://factures.wizall.com/deleteref/6/
```

WOYOFAL
----

### Reload Woyofal

Returns paid electricity meter as json object

- **URL:** /achatwoyofal/
- **Method:** ``POST``
- **URL Params:** None
- **Data Params:** None
	- `msisdn`
	- `compteur`
  	- `amount`
  	- `pincode`
- **Success Response:**
	- **Code:** 200
	- **Content:**

- **Error Response:**
	- **Code:** 401
	- **Content:** ``{ "detail": "Authentication credentials were not provided." }``
	
- **Sample Call:**

```
wget --quiet \
  --method POST \
  --header 'authorization: Token YOUR_TOKEN' \
  --header 'content-type: application/json' \
  --body-data '{ "msisdn":"771234567", "compteur":"58469823", "amount":"1000","pincode": "1001" }' \
  --output-document \
  - https://factures.wizall.com/achatwoyofal/
```

### User electricity meter list
Returns json array of user saved electricity meter

- **URL:** /compteurwoyofal/{phone_number}/
- **Method:** ``GET``
- **URL Params:** None
- **Data Params:** None
- **Success Response:**
	- **Code:** 200
	- **Content:**

```
[
    {
        "id": 22,
        "alias": "Maison",
        "msisdn": 771234567,
        "compteur": 14567634
    }
]
```
- **Error Response:**
	- **Code:** 401
	- **Content:** ``{ "detail": "Authentication credentials were not provided." }``

- **Sample Call:**

```
wget --quiet \
  --method GET \
  --header 'authorization: Token YOUR_TOKEN' \
  --output-document \
  - https://factures.wizall.com/compteurwoyofal/771234567/
```


### Add electricity meter to user collection
Returns added electricity meter details as json object

- **URL:** /compteurwoyofal/
- **Method:** ``POST``
- **URL Params:** None
- **Data Params:**
	- `alias`
	- `msisdn`
	- `compteur`
- **Success Response:**
	- **Code:** 200
	- **Content:**

```
{
    "id": 22,
    "alias": "Maison",
    "msisdn": 771234567,
    "compteur": 14567634
}
```
	
- **Sample Call:**

```
wget --quiet \
  --method POST \
  --header 'authorization: Token YOUR_TOKEN' \
  --header 'content-type: application/json' \
  --body-data '{"alias":"Maison", "msisdn":"771234567", "compteur":"14567634"}' \
  --output-document \
  - https://factures.wizall.com/compteurwoyofal/
```
- **Error Response:**
	- **Code:** 404
	- **Message:** 404 Not Found


### Delete electricity meter from user collection

- **URL:** /deletewoyofal/ID_NUMBER/
- **Method:** ``DELETE``
- **URL Params:** None
- **Data Params:** None
- **Success Response:**
	- **Code:** 200
	- **Content:** None
- **Error Response:**
	- **Code:** 404
	- **Message:** 404 Not Found

- **Sample Call:**

```
wget --quiet \
  --method DELETE \
  --header 'authorization: Token YOUR_TOKEN' \
  --output-document \
  - https://factures.wizall.com/deletewoyofal/22/
```

AIRTIME
----

### Buy airtime

Buy airtime for a phone number

- **URL:** /airtime/
- **Method:** ``POST``
- **URL Params:** None
- **Data Params:** None
	- `msisdn` *Current user phone number*
	- `receveurmsisdn` *Phone number that will receive airtime* 
	- `amount`
	- `reseau` *Network carrier*, possible values are : **ORANGE**, **TIGO**, **EXPRESSO**
- **Success Response:**
	- **Code:** 200
	- **Content:**

- **Error Response:**
	- **Code:** 401
	- **Content:** ``{ "detail": "Authentication credentials were not provided." }``
	
- **Sample Call:**

```
wget --quiet \
  --method POST \
  --header 'authorization: Token YOUR_TOKEN' \
  --header 'content-type: application/json' \
  --body-data '{"msisdn": "771166183","receveurmsisdn": "771234567","amount": "500","reseau": "ORANGE"}' \
  --output-document \
  - https://testfactures.wizall.com/airtime/
```

