# About this release
The release, holds changes to the `POST` `invoices/` and `PATCH` `invoices/{id}` endpoints.

Earlier, there where various properties, that should be set right, when an invoice should be sent, by mail or as an XML document. This has now been collected into a single node named `Send`, that encompasses all the terms that is needed to send an invoice.

## Resend an invoie
The send node has two layouts - a specifiation (request) and a response, where the response holds the same properties as the specification, but adds `ErrorCode` and `ErrorDescription`. When you want FarPay to do something with an invoice, you specifiy the action within the `Send` node.

When you want FarPay do send an invoice by e-mail you have to `PATCH` `invoices/{id}` with the following model:
````javaScript
{
  "Send": {
    "Channel": "email",
    "Status": "Queue",
    "ToAddress": "receiver@company.com",
    "Note": "Greetings, received on the email template as an email note"
  }
}
````
Remark, that the model, is a partial model of the full invoice.


