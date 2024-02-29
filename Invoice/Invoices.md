# Invoices

The invoice endpoint `https://api.farpay.io/{version}/invoices` gives you access to all your invoices. And where you can handle the invoices on the fly, see payment states, and how the invoice is processed in FarPay. Use Case scenarios are:

* List invoices with optional filters
* Single invoice (deep view)
* Create an invoice
* Update invoice
* Delete an invoice

**Remark!** that [all requests must have](../All-Requests.md) an `X-API-KEY` and `Accept` mentioned in the header requests.

# Invoice paymentstates
![State diagram of the invoice](images/invoiceStates/invoiceStates.png)

State | value | Brief description
------|-------|----------------
Not Paid | 100 | Initial state
Paid     | 200 | When a payment as been received and matches the invoice 
Scheduled | 300 | The customer has an agreement, and the invoice will be marked as scheduled
Pending  | 400 | The scheduled payment is now being processed
Rejected | 500 | The payment is being rejected by user, creditor or financial institution
Chargeback | 600 | The amount is charged back, as the monitary transaction is reversed by creditor or finansial institution
Payment failed | 700 | Paymnet failed of various causes such as, agreement was removed, or due to low account balance
N/A  | 1000 |  System errors or errors from the payment systems.


# Get all invoices
The endpoint is available from an `HTTP_GET` at `https://api.farpay.io/{version}/invoices`
Getting the invoices can be done by adding filters optional and independent filters. 
The filters are:
* From DueDate formated as `yyyy-MM-dd` (year-month-day)
* To DueDate formated as `yyyy-MM-dd` (year-month-day)
* PaymentStatus specified with above states, except `N/A`
 
The result is a list of invoice reference, which is a surface presentation of the invoice, its payment status and how it is being processed in FarPay. Remark that the details of the invoice, e.g. invoice lines and further deep details of the invoice is retreived from `https://api.farpay.io/{version}/invoices/{invoiceID}`

Here is an example of a single invoice reference:

````Javascript
[
  {
    "Id": 123,
    "Created": "2017-06-23T13:20:13.852Z",
    "InvoiceNumber": "string",
    "PaymentDueDate": "2017-06-23T13:20:13.852Z",
    "InvoiceAmount": 125,
    "ToBePaidAmount": 125,
    "PaymentReferenceStatus": "Ok",
    "PaymentType": "MobilePayInvoice" || "MobilePaySubscriptions" || 
                   "Betalingsservice" || "Leverandørservice" || 
                   "FI" || 
                   "Dankort" || "Visa" || "MasterCard",
    "SendStatus": "Queue",
    "ErrorDescription": ""
  }
]
````
Property | Description | Valid values
---------|-------------|--------------
Id       | FarPay unique reference to the invoice | `int`
Created  | Timestamp of when the invoice was created | `yyyy-MM-ddThh:mi:ssZ`
InvoiceNumber | The invoice number | `numeric`
InvoiceAmount | The total amount of the invoice, when it was created | `decimal`
ToBePaidAmount | The amount that is to be paid. When partial payments have occur, the reset is stated here | `numeric`
[SendStatus](invoice-send-status.md) | How will the invoice be processed regarding the communication to the customer | status 
ErrorDescription | Describe an occured error | `string`

