[ApiDoc](../Readme) / [Payments](Readme.md) / Payment
# Payment
To see the details of a payment, you can use the `GET` method, and the endpoint `/payments/{paymentID}`.

## Endpoint

| Value    | Desciption                          |
|----------|-------------------------------------|
| Method   | `Get`                               |
| Endpoint | /payments/{paymentId}               |
| Header   | X-API-KEY: {your api key}           |

When you use the endpoint, the response will consist of a JSON object, with the payment details.

## Response
The response is a JSON object, with the following properties:

| Value          | Type     | Description                                                    |
|----------------|----------|----------------------------------------------------------------|
| InvoiceId      | int      | The reference to the invoice, that the payment is related to.  |
| PaymentDate    | DateTime | The date of the payment.                                       |
| ToBePaidAmount | decimal  | The amount that was to be paid.                                |
| PaidAmount     | decimal  | The actual amount that was paid.                               |
| PaymentType    | string   | The payment type.                                              |
| PaymentStatus  | string   | The status of the payment.                                     |
| RefundId       | int      | The reference to the refund, if the payment has been refunded. |
| PaymentId      | int      | The reference to the payment.                                  | 
| PaymentSign    | string   | The sign of the payment. `1` = Payment or `2` = Refund         |


> #### Remark
> The amount is fully paid when the ToBePaidAmount is equal PaidAmount


## Example of a response:
```json
{
  "InvoiceId": 123,
  "PaymentDate": "2018-11-26",
  "ToBePaidAmount": 12.55,
  "PaidAmount": 12.55,
  "PaymentType": "string",
  "PaymentStatus": "string",
  "RefundId": 123,
  "PaymentId": 123,
  "PaymentSign": "1"
}
``` 

