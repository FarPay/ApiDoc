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
* The merchant has a card-creditor-agreement in FarPay
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
`POST https://api.farpay.io/v2/invoices?schedulePayment=Instant`





# Error codes and meaning

code            |  definition                              | call to action
----------------|------------------------------------------|-----------------------------------------
10011           | Card expired, invoice is not received    | Update the card info. Remark the invoice is received when the `schedulePayment` is `default`.
10020           | Payment Rejected, invoice is archived    | Due to GDBR, the reason is not clear. It can be due to the card is locked, or insufficient funds.
10021           | Timeout                                  | The processing did not occur in timely maner. You are kindly asked to perform the action later (e.g. 10 minutes).
 9000           | Authentication failed                    | Contact FarPay support to received guidence for API authentication.
