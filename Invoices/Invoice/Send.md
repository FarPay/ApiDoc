# Send

When an invoice is created, an optional `Send` node can be added, to
send invoices on a different path.

## Properties

| property           | value       | description                                                                                                                                                                                                                  |
|--------------------|-------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `Channel`          | `<type>`    | Send a text message to the user with a given channel<br/><ul><li>`sms`</li><li>`email`</li><li>`xml`</li><li>`print`</li></ul>                                                                                               |
| `Status`           | `text`      |`Queue`, the only valid value, that can be set. Furtuer values are set by the system.                                                                                                                                      |
| `ToAddress`        | `<operand>` | The operands, differ when the channel types are changed. <ul><li>**SMS** is set as a phonenumber</li><li>**Email** is obvious</li><li>**xml** an GLN number</li><li>**print** we need nothing.</li></ul>                     |
| `ScheduleSendDate` | `DateTime`  | The date and time for you need to send this invoice to the customer. It is an approximated schedule, since we are running send-schedules on a minute interval. Peaks can postpone the action in a somewhat shorter interval. |
| `Note`             | `text`      | Remark that adding text to an email is not the same as adding text to an SMS. Adding long texts to an SMS will result in highter charges, due to the size of a single SMS.                                                   |



## Example

I want to send the invoice to a customer on an SMS, at a given time.

```JSON
{
    "Channel": "SMS",
    "Status" : "Queue",
    "ToAddress" : "+4533445566",
    "ScheduleSendDate" : "2024-05-31 15:55",
    "Note" : "Here is your invoice - Cheers!"       
}
```






```

Cheers from FarPay devteam!
This is coded with ❤️ and ☕.

```