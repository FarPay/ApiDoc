# Invoices

The invoice endpoint `https://api.farpay.io/{version}/invoices` gives you access to all your invoices. And where you can handle the invoices on the fly, see payment states, and how the invoice is processed in FarPay. Use Case scenarios are:

* List invoices with optional filters
* Single invoice (deep view)
* Create an invoice
* Update invoice
* Delete an invoice

**Remark!** that [all requests must have](All-Requests.md) an `X-API-KEY` and `Accept` mentioned in the header requests.

# Get all invoices
The endpoint is available from an `HTTP_GET` at `https://api.farpay.io/{version}/invoices`
Getting the invoices can be done by adding filters optional and independent filters. 
The filters are:
* From DueDate formated as `yyyy-MM-dd` (year-month-day)
* To DueDate formated as `yyyy-MM-dd` (year-month-day)
* PaymentStatus can be
   * Not Paid (100)
   * Paid (200)
   * Scheduled (300)
   * Pending (400)
   * Rejected (500)
   * Chargeback (600)
   * Payment failed (700)
   * N/A (1000)
 
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
SendStatus | How will the invoice be processed regarding the communication to the customer | status 
ErrorDescription | Describe an occured error | `string`

# Single invoice
Getting the invoice gives you the relational insights to the customer, the subsequent invoicelines and payment handling. The endpoint is available from an `HTTP_GET` at `https://api.farpay.io/{version}/{invoiceID}`

Here is an example of a detailed invoice, that is due to be paid by Betalingsservice:

````JavasScript
{
  "Id": 12345678,
  "InvoiceDate": "23-06-2017",
  "InvoiceAmount": 100,
  "TaxAmount": 0,
  "ToBePaidAmount": 100,
  "Ean": null,
  "InvoiceNote": "",
  "InvoiceFooter": null,
  "InvoiceWasPaidManually": null,
  "Created": "2017-06-23T08:29:36.057",
  "InvoiceNumber": null,
  "PaymentDueDate": "2017-07-03T00:00:00",
  "Currency": "DKK",
  "Recepient": {
    "CustomerNumber": "1570",
    "Name": "Pernille Badenhofen",
    "Email": "pb@company.dk",
    "Street": null,
    "PostCode": null,
    "PoBox": null,
    "City": null,
    "Country": null
  },
  "Schedule": 0,
  "PaymentStatus": 100,
  "SendStatus": 200,
  "InvoiceStatus": "Ok",
  "PaymentRejectedBy": null,
  "InvoiceLines": [
    {
      "LineNumber": 0,
      "ProductNumber": "1001",
      "Description": "Vores fantastiske produkt",
      "BasePrice": 100,
      "Quantity": 1,
      "DiscountRate": 0,
      "DiscountedPrice": 0,
      "TaxRate": 0,
      "TaxAmount": 0,
      "Amount": 0
    }
  ],
  "TextLines": "Dette er en test\nNy linje"
}
````
# Update invoice
The invoice data cannot be updated, but how the invoice is treated in FarPay can be modified by sending a command to the invoice in order to e.g. re-process the invoice.
The endpoint is available from `PUT` at `https://api.farpay.io/{version}/invoices/{invoiceID}`.

Available operations are:

Operation | description
-------------|------------
Queue        | The invoice is placed in start position, and is now treated with the current settings, available from the sender's company
Sent         | Force the invoice to be treated as sent
ReadyToPrint | The invoice is forced to be set to be printed, and since the printjobs run daily, the status will change from print to sent
Error        | The error state, removes the invoice from the invoice workflow and haltes it - no further actions are executed on the invoices. Later changes can occur e.g. to set on Queue.

# Delete Invoice
The invoice can be marked as deleted by invoking endpoint with `DELETE` at `https://api.farpay.io/{version}/invoices/{invoiceID}`.
The delete action, is equivalent to updateing the invoice to `Error`

