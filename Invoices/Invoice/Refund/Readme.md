# [ApiDoc](../../../Readme) / [Invoices](../../Invoices.md) / [Invoice](../Invoice.md) / Invoice Refund

-----------------

# Invoice Refund

When an invoice paid, a subsequent refund event can be triggered. This document describes the refund event, 
and how it is handled in FarPay.

| Value | Description                      |
|-------|----------------------------------|
| Verb  | POST                             |
| URL   | {baseUrl}/invoices/{id}/download |
| Body  | `"Amount" = 240.50`              |

## Conditions
There are several conditions have to be present, for the invoice to be eligible for a refund.

* The merchant must have a **Card**- or a **MobilePay Recurring** merchant.  
* The invoice must be paid with a refundable paymentoption. Currently they are `card`, `MobilePay Recurring`
* The refundable amount must be equal or less than the original invoice amount.
* The payment that is to be refunded, must comply to the general terms of refundable payments, that might vary over different payment types. Those conditions are outside the scope of of the documentation.

## Example
An invoice has a refund:

**Path**: `https://api.farpay.io/v2/invoices/{id}/refund`
where `{id}` is the reference to the invoice, that you need to perform a refund on.

**Body (in JSON)**:
```JSON
{
  "Amount": 250.50
}
```
**Body in Curl**
````cURL
curl -X POST --header "Content-Type: application/json" --header "Accept: application/json" 
--header "X-API-KEY: mySecretKey" 
-d "{ \ 
   'Amount': 250.50 \ 
 }" \
  "https://api.farpay.io/v2/invoices/{id}/refund"
````


## Result
After the refund has been performed, a message is displayed with how much money has been refunded.