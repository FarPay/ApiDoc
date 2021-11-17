navigate: [ApiDoc](README.md) / [Releases](Releases.md) / API-Release-v2-2021-11-001

# API-Release-v2-2021-11-001
This document describes the release of FarPay API v2, 17th of November 2021

If you have any comments, please reachout to support@farpay.dk and #farpaydev on #slack.

## Document history

state        | author             | timestamp   | description
-------------|--------------------|-------------|--------------------
`Intial`     | @theodorjohannesen | 2021-nov-12 | Initial version
`Ready`      | @theodorjohannesen | 2021-nov-12 | Various corrections
`Ready`      | @theodorjohannesen | 2021-nov-16 | Updating releasedate

## About
The release, holds changes to the `POST` `invoices/` regarding the `paymentSchedule=instant`, scheduled to be deployed 15th of November 2021.

## Breaking changes.
No braking changes will occur - focus is on better return values, when the _instant payment_ occurs.

### Old an new values
This table show the scenarios, the old retur text values, and the new values.

scenario   | old code       | old error message            | new code                | new error message 
-----------|----------------|------------------------------|-------------------------|-------------------------
Timeout    | 100030         | `Betaling fejlet - Afvist af clearhaus, med besked: ''\nKunden bør tilmelde kortet på ny, undersøge kort-aftalen, der er registreret som:\nKunde: Sub 2: Timeout Visa\nKort maske: 100000 XXXX 0099\nTransaktionsbeløb: 75\nTransaktionstidspunkt: 16-11-2021 19:43\nKortet registreret med 3D-secure: True` | 10021 | Instant payment did not process within timelimit. Please try again
Reject     | 100030         | `Betaling fejlet - Afvist af `Indløser`, med besked: 'Rejected test operation'\nKunden bør tilmelde kortet på ny, undersøge kort-aftalen, der er registreret som:\nKunde:  Sub 7: Recurring rejected\nKort maske: 100000 XXXX 0065\nTransaktionsbeløb: 75\nTransaktionstidspunkt: 16-11-2021 19:43\nKortet registreret med 3D-secure: True` | 10020| Instant payment was rejected






## Create an invoice
There are no changes in the input model, nor how an instant invoice is created. But focus is now on returning with a clearer error-message when the processing of an instant payment is not possibile.

Error codes are show in the standard documentation of instant payments, available from: [Instant invoice payment](InvoiceInstantPayment.md).

Currently the version is available from the staging environment: [FarPay Staging API](https://farpay-api-staging.azurewebsites.net/swagger/ui/index)

---

```
Cheers from FarPay devteam!
This is coded with ❤️ and ☕.

tHe0d0r.
```
