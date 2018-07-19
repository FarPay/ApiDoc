# PaymentSets

A Payment set is a collection of payments, grouped by the payment instrument and by day.
The purpose of this presentation is to ease the challenge of aligning the payments on your bankaccount with the payments ledger in your accounting.

**Remark!** that [all requests must have](All-Requests.md) an `X-API-KEY` and `Accept` mentioned in the header requests.

Said that, lets dig into the details. The endpoints are

Method   | Endpoint | Brief description
---------|----------|----------------
`GET`    | https://api.farpay.io/version/paymentsets          | A filtered by date paymentsets are retreived with amount and date 
`GET`    | `https://api.farpay.io/{version}/paymentsets/{id}` | A detailed description of the paymentSet where the customer and the paid amount are shown. When the system was able to pair the customer'  invoice with the amount, the invoice is also specified here





