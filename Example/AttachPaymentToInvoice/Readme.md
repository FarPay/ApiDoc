# Attach an order to a invoice

## Purpose

Creating payment requests are easy, but when the user does not complete the payment flow,
the invoice will be left in a pending payment state.

FarPay has the capability to attach a `Payment` to an `Invoice`, on completion of the payment.
This means that the `Invoice` does not have to be created until, your domain system actually knows
that the payment has been completed.

This article, describes how the `Order` can be expressed, and how to flow towards the paid invoice
is conducted from your domain system.

## Process

The process has the following major steps, that are described in details later in this document:

1. Create an `Order`, expressing the `amount` and `currency` of the payment. It is important that *no customer* is set in the order. FarPay returns the order with a unique
   `Order.Token`
2. Send the `Order.UserUrl` to the paying user/customer, so they can complete the payment.
3. On payment completion, the order transitions `Order.OrderState` from `New` to `PendingCustomerNumber`'
4. As the order changes state, the systems **Fires** a webhook event, stating that now the order is in the new state.

> The current state of the order is that there is a `Payment` attached to the `Order`, and it is awaiting for further
> processing

5. The webhook event is received by your domain system, and you will now create
6. ...an OIO Ubl `Invoice` object ( example available [here](InvoiceExample.md) ),
7. and attach the `Order.Token` from your previous webhook, and attach it to the `Invoice`.
8. Serialize the `Invoice` object to a Base64 encoded string, and post it into the Deliveries endpoint, with the `POST`
   method.

## Goal

The goal of this process is to direct the `Payment` that is currently attached to the `Order`, to the newly created
`Invoice`, as if
it was created, based on the `Invoice` (as a post paid process).

The final result is that now you have a fully documented `Invoice`, with an attached `Payment`, that will be used for
further processing, such as:

* View the customer's Invoice ledger
* Payment expressed in the journal entries of your CRM system.
* Payment can be refunded, and will be processed as a refund in the journal entries of your CRM system.

