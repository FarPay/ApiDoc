navigate: [ApiDoc](README.md) / [Releases](Releases.md) / API-Release-v2-2021-11-001

# API-Release-v2-2021-11-001
This document describes the release of FarPay API v2, 16th of November 2021

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
No braking changes will occur - focus is on better return values, when the instant payment occurs.

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
