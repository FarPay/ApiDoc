# Refund

Refund endpoint is based on an existing refundable payment, that has the status `Paid`, and is not already refunded.

## Endpoint

| Value    | Desciption                              |
|----------|-----------------------------------------|
| Method   | Post                                    |
| Endpoint | /payments/{payment number}/refund       |
| Header   | X-API-KEY: {your api key}               |
| Body     | JSON object with the refund details     |


## Body example
```json
{
  "Amount": 100.00
}
```

# Response
There are two categories of responses, the `Ok` and the `Error` response.

## Ok response
The `Ok` response is returned when the refund is successfully processed. There are some details in the response, that 
vary over different payment providers.


Refund is **not** supported with following payment types:
* FI payment slip
* LS LeverandørService
* BS BetalingsService

How ever, the following payment types are supported:
* MobilePay/Vipps
* Card (Dankort, Visa, MasterCard)

A card refund will result in following response:

```json
{
  "InvoiceId" : 123456,
  "PaymentDate" : "2021-01-01",
  "PaidAmount" : 100.0,
  "PaymentType" : "Dankort" || "Visa" || "MasterCard" || "MobilePaySubscriptions" || "MobilePayInvoice",
  "PaymentStatus" : "Ok",
  "PaymentId" : 123456789,
  "PaymentSign" : "Plus" || "Minus"
}
```

Potential payment statuses are:
* ```New```
* ```Processing```
* ```Ok```
* ```Error```
* ```Ignore```

**Remarks!**
When in ``Error`` no further details are provided. The underlying payment providers hold the reason, but it is not 
expressed in a homogenious way in the response. 

