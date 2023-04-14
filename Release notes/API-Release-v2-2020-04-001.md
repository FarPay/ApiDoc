navigate: [ApiDoc](README.md) / [Releases](Releases.md) / API-Release-v2-2020-04-001
# API-Release-v2-2020-01-001
This document describes the release of FarPay API v2, due medio January 2020. The document is currently in `Draft`, as changes and are expected before the final release.

If you have any comments, please address support@farpay.dk and #farpaydev on #slack.

## Document history

state | author | timestamp | description
------|--------|-----------|-------------
`v.1.0.0` | @theodorjohannesen | 2020-apr-29 | Initial version, adding PaymentDetails to create and get invoice.

## Terms
This document uses the term *FI*, which is the achronym for "Fælles indbetaling" (translated: Common deposit or payment). The FI is a key, that is set on on the invoice og sent by email or printed onto paper. This gives the debtor the ability to use this number, when specifying a monitary transaction in the bank.

An *FI creditor*, is the the company registration, that enables the company to receive FI payments.

## About
The release, holds changes to the `POST` `invoices/` and `GET` `invoices/{id}` endpoints.

## Create an invoice
When the invoice is created, the response has been expanded with the field `PaymentDetails` field on the invoice. The field is a `string`-value, that holds the `FI` value, when the invoice is set to be a manual payment, and an *FI Creditor* is present.
The response shows as follows:

```javascript
{
  ...
  "PaymentType": "FI",
  "PaymentDetails": "+71 <000004561234891 +99995596<",
  ...
}
```
Remark that when the invoice is scheduled as an automatic payment, the FI values not exposed.

## Get an invoice
When retreiving the invoice from the `GET` `invoices/{id}` endpoint, the response has been expaned with `PaymentDetails`. In case of an invoice is marked as `notPaid` in the payment-status, and the creditor (the sender of the invoice) has an FI creditor.

```javascript
{
  ...
  "PaymentType": "FI",
  "PaymentDetails": "+71 <000004561234891 +99995596<",
  ...
}
```
Remark, that the model, is a partial model of the full invoice.
