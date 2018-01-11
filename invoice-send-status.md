# Introduction
The send status indicators determine how the invoice **has been** sent. The key to future events lies within the global company configuration, available from the (settings page)[https://app.farpay.fo/Pages/Settings.aspx]

State     | Value | Description
----------|-------|--------------------------
Queue       | 100   | The invoice has just been created, and is not handled by FarPay yet
PendingApproval  | 110 |
ReadyToPrint | 150 |
Sent | 200 |
Error | 300 |
ErrorSendingEmail | 310 |
WrongEmailAddress | 320 |
EmailBounced | 330 |
EmailMarkedAsSpam | 340 |
EmailRejected | 350 |
MissingEmailAddress | 400 |
NA | 1000 |
NotSent | 9999 |
