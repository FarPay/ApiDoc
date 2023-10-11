# FarPay Order API: Capture of Payment By Request
The [FarPay Order API](https://api.farpay.io/swagger/ui/index#/V2Orders) has introduced a new feature that allows for both automatic and manual capturing of payments associated with an order.
This feature is controlled by the AutoCapture boolean property, which can be set when [Creating (POST)](https://api.farpay.io/v2/orders) an order.

If AutoCapture is set to true, the order is created and payment is captured as soon as the customer enters their payment details. 
On the other hand, if AutoCapture is set to false, the payment is only authorized or reserved when the customer enters their payment details. 
The payment can then be manually captured through the [Capture Endpoint (GET)](https://api.farpay.io/v2/orders/{ordertoken}/capture).

This document will guide you through this process, explaining how each order status is validated and outlining potential violations 
that may occur if the request does not meet the minimum requirements for the requested action.

This section provides a comprehensive guide to understanding possible violations that may occur when operating with the capture flow and potential cancellation thereof. 
Each request, based on its nature, is put through a specific validator.

In the event of a violation, you’ll be presented with a list detailing what is wrong with the order regarding your requested action. 
Each violation is represented by a unique code, a short definition, and a detailed violation message.

This document lists every possible violation, but it’s important to note that not all of them are applicable for each order. 
The violations applicable to an order are determined based on the requested action (Insert/Update/Capture/Cancel), and PaymentTypes (CreditCard/MobilePay) associated with the order.

Please note that as of 13th June 2023, only credit cards are supported for the *request capture scenario*. 
Hence why MobilePay specific violations are not present in the violation list.

## Understanding Violations Regarding Capture or Cancellation of Order.
During the capture flow, and potential cancellation thereof, each request undergoes a specific validation process based on the nature of the request.

If a request fails to meet the minimum requirements for the desired action, you will be provided with a list of violations. 
These violations detail what aspects of the order are incompatible with your requested action.

| Code | Short Definition                       | Violation Message                                                                                                                          |
|------|----------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------|
| 1001 | CaptureHasAlreadyBeenRequested         | Capture has already been requested at {*DateTime*}
| 1002 | MissingCustomer                        | Order is missing customer number
| 1100 | MissingPaymentType                     | No PaymentType present on order
| 1101 | InvalidPaymentType                     | PaymentType {*Current Order PaymentType*} is invalid for capturing this order
| 1200 | OrderNotInPendingCapture               | Order is not ready for capture
| 1201 | InvalidStatusForCapture                | Order is not valid for capture in status: (*Current Order Status*)
| 1202 | InvalidStatusForCancellation           | Order is not valid for cancellation in status {*Current Order Status*}
| 1203 | FlaggedForAutoCapture                  | Order is flagged for AutoCapture
| 1204 | InvalidStatusForAuthorization          | Order is not valid for authorization in status: {*Current Order Status*}
| 1205 | CouldNotDeterminePaymentServiceProvider| Can't continue with the request since Payment Service Provider cannot be determined based on the payment type: {*Current Order PaymentType*}
| 1300 | MissingCardNumber                      | No card number present on order
| 1301 | MissingCardExpire                      | Card expiration date not present on order
| 1302 | CardHasExpired                         | Card has expired. Expiration Date: {*Card Expiration Date*}
| 1400 | MissingPaymentAmount                   | No payment amount present on order
| 1401 | InvalidPaymentAmount                   | Payment amount cannot be zero or negative. Amount listed: {*Current Order Amount*}
| 1500 | MissingPaymentTransactionId            | No payment transaction id present on order
| 1501 | MissingCallbackUrl                     | No callback url present on order
| 5000 | PspError                               | Error From Payment Service Previder: {*Error Message From PSP*}
| 5001 | CaptureReflectError                    | Capture was performed, but the FarPay Order does not reflect this. Please contact FarPay.
| 6001 | AlreadyCancelled                       | Order has already been cancelled
| 6002 | CancelReflectError                     | Cancel request was performed, but the FarPay Order does not reflect this. Please contact FarPay.

*As of 13th June 2023 only credit cards are supported. Hence why MobilePay specific violations are not present in the violation list.*

For example: Violation codes **1300, 1301, 1302** are only ever taking into the validation process if the PaymentType is associated with a CreditCard and never if MobilePay.

***
## Order Status

| Code  | Status                 |
|-------|------------------------|
| 100   | New                    |
| 160   | PendingCustomerNumber  |
| 170   | PendingCapture         |
| 190   | Processing             |
| 200   | Ok                     |
| 300   | Error                  |
| 400   | Cancelled              |

### New
Indicates that the order has been successfully created and is awaiting further actions.

### PendingCustomer
Signifies that the customer has entered their payment details, but the order is still missing a *"CustomerNumber”*.

### PendingCapture
Indicates that the system is ready to capture the reserved payment from your customer. 

### Processing
The *“Processing”* status is an intermediate state that persists until we receive a callback from the PSP. 
The callback will provide information about the capture operation’s success or failure. 
It’s important to note that the duration of this “Processing” state can vary and is dependent on the PSP’s response time.
Once the PSP’s response is received and processed, the order will be updated accordingly to reflect the final outcome of the capture operation.

### OK
The payment, and agreement if applicable, have been successfully created and captured. The order has now completed its lifecycle.

### Cancelled
The order and all its associated elements have been cancelled.

### Error
An error has occurred, ending the order’s lifecycle. No further action can be taken at this point.

***
## Creating an order
An order is initiated with an API Request via the [Create Order (POST)](https://api.farpay.io/v2/orders) endpoint.

Upon creation, the order is given the “New” status. 
The response to this request will include this status, along with other general information such as the uniquely generated “OrderToken”. 
This token is used for all future requests pertaining to this specific order.

The response also includes a *“UserInputUrl”* property. 
This URL provides access to the *FarPay Payment Window* associated with the newly created order. 
You can share this URL with your customer to allow them to input their payment details.

Once payment details are received, the order status will be updated to either *“PendingCustomerNumber”* or *“PendingCapture”*. 
If the order was created without a *“CustomerNumber”* in the request body, it will be assigned the *“PendingCustomerNumber”* status. Otherwise, it will be assigned the “PendingCapture” status.

## Updating an order
Before the payment associated with an order can be captured, the order requires customer information. 
If a customer number already exists, that customer will be associated with the order. Otherwise, a new customer will be created.

The order must be updated with a *“CustomerNumber”* via [Update Order Endpoint (PUT)](https://api.farpay.io/v2/orders).

## Cancelling an order
Order cancellation is possible only when the order is in the *"New"*, *"PendingCustomerNumber"*, or *"PendingCapture"* statuses. 
This can be done via the [Cancel Order (GET)](https://api.farpay.io/v2/orders/{ordertoken}/cancel) endpoint. If the order is not in one of these statuses, you will receive a Violation Response.

The cancellation process varies depending on the OrderStatus, but it will trigger a series of actions as described below:

- *New*: The order will be moved to the “Cancelled” status. No further action is taken since there are no payment details associated with the order yet.

- *PendingCustomerNumber*: The order will be moved to the “Cancelled” status and any payment details associated with the order will also be cancelled. If an agreement is part of the order, the external payment agreement will be cancelled as well.

- *PendingCapture*: The order will be moved to the “Cancelled” status and any payment details associated with the order will also be cancelled. If an agreement is part of the order, the external payment agreement will be cancelled as well. Furthermore, since “PendingCapture” implies that a CustomerNumber is present and associated with the order, if there is an agreement present on the order, the customer’s link to that agreement will be cancelled.

Please note that any status other than those listed above will result in a Violation Response.

## Capturing an Order
Order capture is possible only when the order is in the *“PendingCapture”* status, and this can be done via the [Capture Endpoint (GET)](https://api.farpay.io/v2/orders/{ordertoken}/capture).

If the order status is *“Error”*, *“PendingCustomerNumber”*, or *“Ok”*, no capture request will be performed and the order status will remain unchanged. In these cases, you will receive a Violation Response.

For any other status apart from “PendingCapture”, the order status will be updated to “Error” and you will receive a Violation Response.

Upon a successful capture request, the order will be updated as follows:
- The OrderStatus will be set to *"Processing"*.
- The CaptureRequestedAt will be marked with the current date and time.

You will then receive a standard order response that includes these updated values.
***