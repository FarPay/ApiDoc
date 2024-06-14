Breadcrumbs: [Orders](Readme.md) / [Order](Readme.md) / [Order POS](order.pos.md)

----------
# Order POS
Creating an order, for POS purposes, focus in on the purpose of the order, where the path to a payment in 
combination with a recurring mandate must be frictionless.

## MobilePay POS scenario

The MobilePay POS scenario is where an order is created to enforce a recurring mandate.

## Preconditions

The following preconditions must be met, before the order can be created:

* Merchant has Vipps Recurring
* Customer has the Vipps App
* Customer is eligible for a recurring mandate in the subsequent bank account.

## Action
When creating an order, following conditions must be met:
* ``Agreement = 1`` (Mandatory)
* ``Type = mp``
* URL: (Verb and URI) `POST` to `{baseUrl}/Orders/{version}`

### Example
To initiate a POS scenario asking the customer to create a MobilePay Mandate, will occur with or without a 
predefined customer. 

First, an order without a customer:

```json
{
  "ExternalID": "YourReference",
  "AcceptUrl": "https://httpbin.org/anything?FarPayStatus=Accepted",
  "CancelUrl": "https://httpbin.org/anything?FarPayStatus=Cancelled",
  "CallbackUrl": "https://webhook.site?....",
  "Lang": "da",
  "PaymentTypes": "mp",
  "Agreement": 1
}
```

And with a `Customer.CustomerNumber`

```json

{
  "ExternalID": "YourReference",
  "AcceptUrl": "https://httpbin.org/anything?FarPayStatus=Accepted",
  "CancelUrl": "https://httpbin.org/anything?FarPayStatus=Cancelled",
  "CallbackUrl": "https://webhook.site?....",
  "Lang": "da",
  "PaymentTypes": "mp",
  "Agreement": 1,
  "Customer": {
    "CustomerNumber": "123123"
  }
}
```

### Result
The result of the process is a response with a `UserInputUrl`, that holds the URL to the POS scenario.
In the case of MobilePay Recurring, a screen will show a screen with a phonenumber input field, and a timer, counting 
down from 5 minutes (or some other configured timespan).
