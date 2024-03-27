navigate: [ApiDoc](../README.md) / [Invoices](Invoices.md) / Invoice Instant Paymnet

# Invoice Instant Paymnet

When the `schedulePayment = Instant`, the system changes the payment behaviour accordingly. This document describes the error, that can encounter when executing this behaviour.
Other behaviours 

# Terms and definitions

Here are the terms, that are used in this article, that the reader must be familiar with.

Term              | Definition                                  
------------------|----------------------------------------------
merchant          | The company, that has access to FarPay       
customer          | The end user, that pays the invoice (Debtor) 
card subscription | A card, that is registered with the recurring option


# Preconditions
When an instant payment is executed, there are following preconditions, that are challenged on execution time:
* The merchant has a card-creditor-agreement in FarPay, and it must be enabled to handle subscriptions.
* The customer has an active card with recurring/subscription ability, attached in FarPay
* The request must be expressed with the `scheduledPayment = instant` to complete such a request
* The card subscription must be valid 
  * Preferably created with 3D-secure
  * Have suffucient funds
  * Not closed, due to theft or other reasons
 
## Conditions for instant payment
There are following conditions for an instant payment:
* The creditor card agreement must have recurring set as a valid option.
* The customer must have an active card recurring paymentoption
* The request must be expressed with the scheduled = instant to complete such a request.

## Example of an invoice with Instant payment
The datamodel is the same as posting a regular invoice model. But when posting into the `/invoices` endpoint, you must include the queryparameter: `schedulePayment=Instant`
As an example with v2 as version, the request would look like this:
`POST https://api.farpay.io/{version}/invoices?schedulePayment=Instant`
Example body is available from: (Post single invoice)[Invoices.md#single-invoice]


# Error codes and meaning
In addition to the standard `POST Invoies` endpoint, these errorcodes are handled on instant payment.

code            |  definition                              | call to action
----------------|------------------------------------------|-----------------------------------------
10011           | Card expired, invoice is not received    | Update the card info. _Remark!_ This error code is only sent when the `schedulePayment` is `instant`, 
10020           | Payment Rejected, invoice is archived    | Due to GDPR, the reason for the rejection is not clear. It can be due to the card is locked, or insufficient funds.
10021           | Timeout, invoice is archived             | The processing did not occur in timely maner. You are kindly asked to perform the action later (e.g. 10 minutes).

## Elaboration of status codes
### Timeout
Timeout occurs when the timelimit of approximately 20-30 seconds are exeeded. Subsequent actions are managed from FarPay, that cancels the reservation, so that the reservation will be cancelled within a few minutes, on the customer bank account.

### Payment Rejected
A rejection occurs when the card somehow is not eligible for an instant capture of the given amount. Due to GDBR, FarPay is not informed about the details, regarding of why the card was rejected. But following states do occur, and can be managed by the merchant or the debtor.
* Locked card
* Missing 3D-Secure autorization (SMS or NEM-ID autorization)
* Insufficient funds

Other errors are more specific and technical, where the debtor must contact the financial institution (or bank), to cover the details. FarPay and the seleced PSP are not in posession of further details, relating to the error.
