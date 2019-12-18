navigate: [ApiDoc](README.md) / [Releases](Releases.md) / API-Release-v2-2020.
# API-Release-v2-2020-01-001
This document describes the release of FarPay API v2, due medio January 2020. The document is currently in `Draft`, as changes and are expected before the final release.

If you have any comments, please address support@farpay.dk and #farpaydev on #slack.

## Document history

state | author | timestamp | description
------|--------|-----------|-------------
`Draft` | @theodorjohannesen | 2019-dec-18 | Initial version, mentioning the Send node.


## About
The release, holds changes to the `POST` `invoices/` and `PATCH` `invoices/{id}` endpoints.

Earlier, there where various properties, that should be set right, when an invoice should be sent, by mail or as an XML document. This has now been collected into a single node named `Send`, that encompasses all the terms that is needed to send an invoice.

## Create an invoice
When an invoice is created, the `Send` node can contain a specification of what send action is needed. In the example blow and others to come, the focus is only on this node, as a partial `invoice` model.

This will set the invoice in the send-email-queue, and will subsequently sent as planned.

```javascript
{
  "Send": {
    "Channel": "email",
    "Status": "queue",
    "ToAddress": "receiver@company.com",
    "Note": "Greetings, received on the email template as an email note"
  }
}
```
And when you want to send the invoice as an XML document to the receiver. Here the `ToAddress` holds the receiver GLN value (GLN= Global location number).

```javascript
{
  "Send": {
    "Channel": "xml",
    "Status": "queue",
    "ToAddress": "57450000001",
    "Note": ""
  }
}
```

## Resend an invoie
The send node has two layouts - a specifiation (request) and a response, where the response holds the same properties as the specification, but adds `ErrorCode` and `ErrorDescription`. When you want FarPay to do something with an invoice, you specifiy the action within the `Send` node.

When you want FarPay do send an invoice by e-mail you have to `PATCH` `invoices/{id}` with the following model:

````javascript
{
  "Send": {
    "Channel": "email",
    "Status": "queue",
    "ToAddress": "receiver@company.com",
    "Note": "Greetings, received on the email template as an email note"
  }
}
````

Remark, that the model, is a partial model of the full invoice.


## Minor changes
Other changes, that can be mentioned in bullits are...
* The endpoint to handle the refund has been given a new HTTP-Verb. Now it is available from: `POST` `/invoices/{id}/refund`
* In `POST` `invoices`, the property `SendStatus` has been removed, where this info is available from the `Send` node. 

