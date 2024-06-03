### [Home](../../../README.md) > [Orders](../../Readme.md) > [Response](ReadMe.md) > Bad Request

--------------------------------

# Bad Request

| Term               | Value                 |
|--------------------|-----------------------|
| Http response code | 400 (BadRequest)      |
| Body               | An ApiResponseMessage |


## ApiResponseMessage
The response message, holds the key values, that express the error, 

| Property      | Description                                              |
|---------------|----------------------------------------------------------|
| Message       | A description of the error, and what caused it           |
| CorrelationId | The GUUID, that can be used to troubleshoot the scenario |
| Details       | A collection of violations                               |

## Violation
A violoation is an identification of a specific requirement, that is not met as FarPay has received a request 
of creating an [Order](../../Readme.md).

### List of violations
The list of violations are expanded, as the [Order](../../Readme.md) grows in capability. 

| Code       | Title                                         | Description                                                                                                           | 
|------------|-----------------------------------------------|-----------------------------------------------------------------------------------------------------------------------|
| ```1001``` | ```CaptureAlreadyRequested```                 | "Capture has already been requested at {0}";                                                                          | 
| ```1002``` | ```MissingCustomer```                         | "Order is missing customer number";                                                                                   | 
| ```1100``` | ```MissingPaymentType```                      | "No PaymentType present on order";                                                                                    | 
| ```1101``` | ```InvalidPaymentType```                      | "PaymentType ({0}) is invalid for capturing this order";                                                              | 
| ```1200``` | ```OrderNotInPendingCapture```                | "Order is not ready for capture";                                                                                     | 
| ```1201``` | ```InvalidStatusForCapture```                 | "Order is not valid for capture in status: {0}";                                                                      | 
| ```1300``` | ```MissingCardNumber```                       | "No card number present on order";                                                                                    | 
| ```1301``` | ```MissingCardExpire```                       | "Card expiration date not present on order";                                                                          | 
| ```1302``` | ```CardHasExpired```                          | "Card has expired. Expiration Date: {0}";                                                                             | 
| ```1400``` | ```MissingPaymentAmount```                    | "No payment amount present on order";                                                                                 | 
| ```1401``` | ```InvalidPaymentAmount```                    | "Payment amount cannot be zero or negative. Amount listed: {0}";                                                      | 
| ```1500``` | ```MissingPaymentTransactionId```             | "No payment transaction id present on order";                                                                         | 
| ```1501``` | ```MissingCallbackUrl```                      | "No callback url present on order";                                                                                   | 
| ```1202``` | ```InvalidStatusForCancellation```            | "Order is not valid for cancellation in status {0}";                                                                  | 
| ```1203``` | ```FlaggedForAutoCapture```                   | "Order is flagged for AutoCapture";                                                                                   | 
| ```1204``` | ```InvalidStatusForAuthorization```           | "Order is not valid for authorization in status: {0}";                                                                | 
| ```1205``` | ```CouldNotDeterminePaymentServiceProvider``` | "Can't continue with the request since Payment Service Provider cannot be determined based on the payment type: {0}"; | 
| ```5000``` | ```PspError```                                | "Error From Payment Service Provider";                                                                                | 
| ```5001``` | ```CaptureReflectError```                     | "Capture was performed, but the FarPay Order does not reflect this. Please contact FarPay.";                          | 
| ```6001``` | ```AlreadyCancelled```                        | "Order has already been cancelled";                                                                                   | 
| ```6002``` | ```CancelReflectError```                      | "Cancel request was performed, but the FarPay Order does not reflect this. Please contact FarPay.";                   | 
| ```7001``` | ```MissingOneOffPaymentId```                  | "Can't capture order due to missing MobilePay OneOff PaymentId not present on order";                                 | 
| ```7002``` | ```MissingMobilePayAgreement```               | "Order is not associated with an active MobilePay Agreement";                                                         | 


Remark that the string is formatted with input parameters, that express the current situation.

 
## A generated example of an error

```javJavascript
{
    "Message" : "description of a message",
    "CorrelationId" : LogGuuid,
    "Details" : [
        {
            "Code" : 1234,
            "Message" : "Expression of the error",
            "Details" : [
                {
                    "Key" : "myKey1",
                    "Value" : "My value for key 1"
                },
                {
                    "Key" : "myKey2",
                    "Value" : "My value for key 2"
                },
                ...
            ]
        },
        {
            "Code" : 5678,
            "Message" : "Expression of the error",
            "Details" : [
                {
                    "Key" : "myKey1",
                    "Value" : "My value for key 1"
                },
                {
                    "Key" : "myKey2",
                    "Value" : "My value for key 2"
                },
                ...
            ]
        },
        ...
    ]     
}

```