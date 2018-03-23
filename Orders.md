
# Orders

The orders endpoint

The invoice endpoint `https://api.farpay.io/{version}/orders` gives you access to all your orders, and their state. Use Case scenarios are:
* List orders with optional status filter
* Single order (deep view)
* Create an order
* Update the order

**Remark!** that [all requests must have](All-Requests.md) an `X-API-KEY` and `Accept` mentioned in the header requests.

# Order status
![State diagram of the order](orderStates.png)

State                 | value | Brief description
----------------------|-------|------------------------------------------------
New                   | 100   | Initial state
PendingPayment        | 200   | When a payment as been received and matches the invoice 
PendingCustomerNumber | 300   | The customer has an agreement, and the invoice will be marked as scheduled
Ok                    | 400   | The scheduled payment is now being processed
Error                 | 500   | The payment is being rejected by user, creditor or financial institution
Canceled              | 600   | The amount is charged back, as the monitary transaction is reversed by creditor or finansial institution
Expired               | 700   | Paymnet failed of various causes such as, agreement was removed, or due to low account balance

# Get all orders
The endpoint is available from an`HTTP_GET` at `https://api.farpay.io/{version}/orders`, and can be filtered statusvalues mentioned in the table above.

Here is an example of a collection wiht an order - Remark that this is an example presented in JSON, and that the data can be presented as SOAP XML if requested...
````Javascript
[
  {
    "Token": "abc123",
    "ExternalID": "your reference",
    "AcceptUrl": "https://companyName.com/acceptUrl",
    "CancelUrl": "https://companyName.com/cancelUrl",
    "CallbackUrl": "https://companyName.com/callbackUrl",
    "Lang": "en",
    "CustomerNumber": "1234567890",
    "CustomerName": "Customer Name",
    "CustomerEmail": "email@address.com",
    "Payment": {
      "Amount": 49.95,
      "Currency": "DKK",
      "Description": "First half month payment",
      "Reference": "YourPaymentReference"
    }
  }
]
````
Property | Description | Valid values
---------|-------------|--------------
Token    | FarPay unique token to the order | `string`
ExternalID | Your domain reference to the order in FarPay | `string`
AcceptUrl | Url, when the order is successfully completed | `string`
CancelUrl | Url, when the user cancels the order | `string`
CallbackUrl | Url for delivery data when the user completes the registration | `string`
Lang | Language specification can be `en` for english, `da` for danshh, `fo` for faroese | `string`
CustomerNumber | Customer number | `string`
CustomerName | Name (first and last) of the customer | `string`
CustomerEmail | Customer E-mail | `string`
Payment-Amount | Payment with . seperator for decimals | `decimal`
Payment-Currency | Currency in standard ISO 4217 format | `string`
Payment-Description | Describe what the customer is paying for | `string`
Payment-Reference | Your domain reference to the payment | `string`
