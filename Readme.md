# Welcome
The API is documented with the Swagger framework, where focus is on creating an API that is available for test, and usage, right after you have gained access. This document, and in combiniation with the swagger framework should promote a shortend learningcurve.

Lets kick this off by aligning some general terms of the API:
* The terms are business driven - that is terms that non-technical person should understand.
* The API is versioned with a versionnumber is attached to the root URL. Noted as a post fix notation https://api.farpay.io/ `<version number>`
* All endpoints are authenticated with an API key. See [how to get an API key](Api-Key-Get.md) 
* All endpoints have an `HTTP_GET` method, that return a collection of the corresponding object, or in some cases, a reference-object, which is a minimum presentation of a larger business object.
* All endpoints have a *sub-child* HTTP_GET method, that returns a single object, that is further elaborated in details and relations. One example is the invoice. The invoice is grabbed from the `https://api.farpay.io/invoices/<invoice ID>`, where the `<invoice ID>` identifies that specific invoice.
* All endpoints are testable in the swagger UI, by [entering the API-Key](API-Key-Input.md) or by [adding the request headers](All-Requests.md). 
* Date is rendered in two formats. The *input* date is given as `yyyy-MM-dd`, while a date result is rendered as `yyyy-MM-ddThh:mi:ssZ`
* Other endpoints depending the http-verb, such as `POST`, `PUT`, `PATCH` or `DELETE`, depending on the available functional scope. Furher info on these, where you dive in.
* The Examples are encompassing the list of complex integration examples, that can be used as the final point in your
  integration. The examples are available in the [Examples folder](Example/Readme.md).

## Root URL
The url is 
```
https://api.farpay.io
```

## Version
After the Url, You have to determine the version. Current version is `v2`
```
https://api.farpay.io/v2
```

### Release notes
Release notes are available in the an accumulation : [Release notes](Releases.md)

## Table of objects
Each object is described in this hub, and available from our testable Swagger API 

| Term          | Swagger | Description |
| :---          |        ---: |     ---:|
| Customers     | [Customers](https://api.farpay.io/swagger/ui/index#/Customers) | [Customers](/Customers) |
| Agreements    | [Agreements](https://api.farpay.io/swagger/ui/index#/Agreements) | [Agreements](Agreements.md) |
| Invoices      | [Invoices](https://api.farpay.io/swagger/ui/index#/Invoices) | [Invoices](/Invoices/Invoices.md) |
| Payments      | [Payments](https://api.farpay.io/swagger/ui/index#/Payments) | [Payments](/Payments) |
| Subscriptions | `Deprecated` | `Deprecated` |
| Orders        | [Orders](https://api.farpay.io/swagger/ui/index#/Orders) | [Orders](/Orders) |
| Deliveries    | [Deliveries](https://api.farpay.io/swagger/ui/index#/Deliveries) | [Deliveries](/Deliveries) |

This document focuses on explaining of how the developer can get started by testing with an API-Key, and by testing, see how the API works and how it is used by staging simple examples to 

The swagger document is available from: 

```
https://api.farpay.io/swagger/docs/v2
```

The swagger GUI, for browsing and testing is available from: https://api.farpay.io/swagger - And a short description of [swagger](http://swagger.io/docs/specification/what-is-swagger/) for further reading.

The first version of the api is now [legacy](README-Legacy.md).

## Trial
You are welcome to try FarPay for free, by [applying](https://www.farpay.io/prov/) on our webpage. Afterwards, you are welcomed to apply for an API-Key by sending a request in our chat.

Now the all the general stuff has been aligned, let's go into the details. View this document of *how to* get started, and the *swagger* document as the detailed document of how the *endpoints are reached*.

# Additional info
Since users of the API are *business users* or *enterprise users*, they get an extra access to your support-and-ticket system, where issue, needs and wants can be described or raised. 
