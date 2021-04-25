### Definitions

Term | Elaboration
--------------|------------------------------------
_Customer_    | Is the person or business, that receives an invoice from your comapny, and can by using the presented payment technology, pay an invoice or subscribe to a payment technology.
_Payment intrument_ | Gives the _customer_ the ability to pay an amount to your comapny

# Customers
The customers endpoint is your access to the FarPay customer database.
Use case scenarios are:
* Get all customers
* Get a single customer, with a recurring payment instrument details
* Create a new customer
* Update existing customer
* Send an invitation email to the customer, so that the customer can create a recurring payment instrument.

Remark that [all requests must have](All-Requests.md) an `X-API-KEY`, and a `Accept` mentioned in the header of the request.

# Get all customers
Use the `https://api.farpay.io/v2/customers` for retreiving all customers. The objects hold all the details

# Get a single customer
Use the `https://api.farpay.io/v2/customers/{customer number}` e.g. with customer number= 23.

# Create a new customer
To create a customer, the endpoint accepts both XML and JSON as payload of the customer data. In this example JSON is used.
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
monitoring the customer when the invoice is opend, or when downloaded are with this setting inaccurate.

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
AttachPdfInvoice | Customer gets PDF-attachements on invoices | boolean
Language | Communication langauge | "Danish", "English", "Faroese", "Norwegian"


# Update an existing customer
The customer can be updated by a `PUT` from `https://api.farpay.io/v2/customers/`
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

# Send an email for creating a payment agreement
When you want FarPay to send an email to your customer with the ability to create a recurring payment instrument, the
endpoint `GET` to `https://api.farpay.io/v2/customers/{customer number}/agreementRequest?type={type}&email={email}'`
There are three parmeters that must be set when making this call:

Parameter name    | Values                                           | Placeholder
------------------|--------------------------------------------------|------
`customer number` | the customer number, that is used in the URL     | Route
`type`            | `mp`, `card`, `bs`, `ls`or `all`                 | Uri
`email`           | the email address                                | Uri

## Type values and definition

The type sets what payment instrument shoul be shown, when the customer creates a payment agreement. See values, and the description below.

Value | description
-------|----------------------------------------------------------------------------------
`mp`   | MobilePay Subscriptions payment agreement.
`card` | Card agreement - Can be Visa, MasterCard or Dankort
`bs`   | Betalingsservice - Direct debit account information, *mainly* for private customers
`ls`   | Leverandørservice - Direct debit account information, business only
`all`  | When multiple payment types available, the customer selects a favorable. 

Back to the [overview](README.md#program-dokumentation)
