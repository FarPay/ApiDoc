# Introduction
The send status indicators determine how the invoice **has been** sent. The key to future events lies within the global company configuration, available from the [app settings page](https://app.farpay.fo/Pages/Settings.aspx)

| State               | Value | Description                                                                                                       |
|---------------------|-------|-------------------------------------------------------------------------------------------------------------------|
| Queue               | 100   | The invoice has just been created, and is not handled by FarPay yet                                               |
| PendingApproval     | 110   | Future states for invoices that have approval workflow                                                            |
| ReadyToPrint        | 150   | The invoice is placed in a printqueue, due to configuration or automatically, due to missing email address        |
| Sent                | 200   | The invoice has been sent                                                                                         |
| Error               | 300   | The invoice is halted, and will not be processed                                                                  |
| ErrorSendingEmail   | 310   | The system was not able to send the email address, due to technical issues e.g. bad connection to the SMTP server |
| WrongEmailAddress   | 320   | No mailbox was found with that name                                                                               |
| EmailBounced        | 330   | Email bouncing due to e.g. full mailbox.                                                                          |
| EmailMarkedAsSpam   | 340   | The email was sent, but marked as spam                                                                            |
| EmailRejected       | 350   | The invoice was rejected                                                                                          |
| MissingEmailAddress | 400   | Email address was missing.                                                                                        |
| NA                  | 1000  | When the general configuration indicates that nothing is to be sent to this customer.                             |
| NotSent             | 9999  | The invoice will not be sent                                                                                      |
