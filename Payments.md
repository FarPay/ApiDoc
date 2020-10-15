[ApiDoc](README.md) / Payments

# Payments

The Payments endpoint, available from `https://api.farpay.io/{version}/Payments` is the endpoint where you can see the payment history over a given time, as well as filtering over an `invoiceID`.
With the endpoint, you can:
* Get all - Filter payments, based on from and to date, or an invoiceID
* Get single - Get a single payment info
* Refund - Refund a card payment.

**Remark!** that [all requests must have](All-Requests.md) an `X-API-KEY` and `Accept` mentioned in the header requests.

# Get All 
This endpoint filters existing payments, based on:
* `paymentDateFrom` - begin date, format as 'YYYY-MM-DD'
* `paymentDateTo` - begin date, format as 'YYYY-MM-DD'
* `invoiceID` - unique reference to an invoice
* `paymentReference` - payment reference is set on orders' payments.

The meaningfull combination is based on the two paymentDate variables. `invoiceID` and `paymentReference` should not be initialized in combination with the other properties.

# Get a single payment 

The single payment accesspoint is available from `https://api.farpay.io/{version}/Payments/{paymentId}`, where you can retreive a single payment-node, and the same degree of details as the Get All endpoint.

# Refund
The refund endpoint is available from: `https://api.farpay.io/{version}/Payments/{paymentId}/refund/{amountInMinorUnits}`.
The `paymentId`, needs to be a refundable payment, and the amount, given in minor units (or cents), must be less then the original payment and earlier refunds.

**Remark!** that the refund endpoint only features refund of card payments.

# Result
This result is returned in all instances, where a successfull call to the Payments endpoint is performed.

````Javascript

[
  {
    "InvoiceId": 123,
    "PaymentDate": "2018-11-26",      // Formated: YYYY-MM-DD
    "ToBePaidAmount": 12.55,          // Amount with 2 decimal places
    "PaidAmount": 12.55,              // Amount with 2 decimal places
    "PaymentType": "string",          // Available payment types are : 
                                      // MobilePayInvoice, MobilePaySubscriptions, 
                                      // BS, LS, FI, Visa, MasterCard, Dankort
    
    "PaymentStatus": "string",        // Paid, PaymentRejected, ReimbursedByBank,
                                      // PaymentOptionCanceled, PaymentFailed
    "PaymentId": 123,                 // Unique reference to the payment.
    "PaymentSign": "string"           // Payment || Refund
  }
]

````

The result is a collection of payments, as the result of the query. The collection can hold zero to many items.

