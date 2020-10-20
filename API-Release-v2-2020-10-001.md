navigate: [ApiDoc](README.md) / [Releases](Releases.md) / API-Release-v2-2020-10-001
# API-Release-v2-2020-10-001
This document describes the release of FarPay API v2, 20'th of October 2020.

If you have any comments, please address support@farpay.dk and #farpaydev on #slack.

## Document history

state | author | timestamp | description
------|--------|-----------|-------------
`v.1.0.0` | @theodorjohannesen | 2020-oct-20 | Initial version

## Terms
This document uses the term *FI*, which is the achronym for "Fælles indbetaling" (translated: Common deposit or payment). The FI is a key, that is set on on the invoice og sent by email or printed onto paper. This gives the debtor the ability to use this number, when specifying a monitary transaction in the bank.

An *FI creditor*, is the the company registration, that enables the company to receive FI payments.

## About
The release, holds changes to the `POST` `invoices/`

## Create an invoice
The submitted model with `invoice.TextLines` are persisted. Other text related fields are also changed in the release. They are...
* `invoice.InvoiceNote`, a note, that is set on the invoice, and presented on the bottom of the invoice PDF
* `invoice.Send.Note` - An extra message, that is set on the email or SMS, that is sent to the customer with the 

When the invoice is sent to Betalingsservice, where the `TextLines` are used to print the BS statement. And the `InvoiceNote` is used as an appended text to the Betalignsservice statement.
