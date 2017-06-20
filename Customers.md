# Customers
The customers endpoint is your access to the FarPay customer database.
Use case scenarios are:
* Get all users
* Get a single user, with a recurring payment instrument details
* Create a new user
* Update existing user
* Send an invitation email to the user, for the user can create a recurring payment instrument.

Remark that [all requests must have](All-Requests.md) an `X-API-KEY`, and a `Accept` mentioned in the header of the request.

# Get all users
Use the `https://api.farpay.io/v2/customers` for retreiving all customers. The objects hold all the details

# Get a single user
Use the `https://api.farpay.io/v2/customers/23` for retreiving the customer with customernumber = 23

# Create a new user
To create a user, the endpoint accepts both XML and JSON as payload of the customer data. In this example JSON is used.
*Remark* that the customer object has a minimum set of required properties, for the system to be used fully. 
They are:
* CustomerNumber
* Name
* Email

```javascript
{
  "CustomerNumber": "string",
  "Name": "string",
  "Email": "string",
  "PoBox": "string",
  "Street": "string",
  "AdditionalStreet": "string",
  "HouseNumber": "string",
  "PostCode": "string",
  "City": "string",
  "Country": "string",
  "AttachPdfInvoice": false,
  "Language": "Danish"
}
```

The `AttachPdfInvoice` is used when you want to distribute the PDF-invoice with the invoice email. Remark that the common log of
monitoring the user when the invoice is opend, or when downloaded are with this setting inaccurate.

The `Language` setting should only be used for language variations, meaning of your company communicates in one language, the 
customers who read the same language, do not need this property to be set, while others can.

Properties | Description | type
-----------|-------------|--------------------------------------------------
CustomerNumber | Unique customer identifier | numeric value max 15 digits
Name | The given name of the customer | 255 characters
email | communcation to the customer | 255 characters
PoBox | post box | 20 characters
Street | Address or streetname | 255 characters
AdditionalStreet | Additional addressline | 255 characters
HouseNumber | Supplementary address info | 10 characters
PostCode | Post district or area | 20 characters
Country | Country | 255 characters
AttachPdfInvoice | User gets PDF-attachements on invoices | boolean
Language | Communication langauge | "Danish", "English", "Faroese", "Norwegian"


# Update an existing user
The user can be updated by a `PUT` from `https://api.farpay.io/v2/customers/`
Compared to the create, there are some limitations of what can be updated.
The updates can be done on:
* Name
* All the address properties
* Email
* AttachPdfInvoice
* Language

An example update could be an norewgian customer, now residing in the UK: 
```javascript
{
  "CustomerNumber": "string",
  "Name": "John Smith",
  "PoBox": "2301",
  "Email": "my@company.co.uk",
  "Street": "Marksquare",
  "AdditionalStreet": "Wellington st.",
  "HouseNumber": "4",
  "PostCode": "3422",
  "City": "Bristol",
  "Country": "United Kingdom",
  "AttachPdfInvoice": false,
  "Language": "Norwegian"
}
```

Back to the [overview](GeneralInfo#program-dokumentation)
