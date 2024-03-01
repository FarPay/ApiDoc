Breadcrumbs: [Orders](OrdersOverview.md) / [Order](Order.md) / [Order POS](Order.POS.md)

----------
# Order POS
Creating an order, for POS purposes, focus in on the purpose of the order, where the path to a payment in 
combination with a recurring mandate must be frictionless.

## MobilePay POS scenario

The MobilePay POS scenario is where an order is created to enforce a recurring mandate.

## Preconditions

The following preconditions must be met, before the order can be created:

* Merchant has Vipps Recurring
* Customer has the Vipps App
* Customer is eligible for a recurring mandate.

## Action
When creating an order, following conditions must be met:
* ``Agreement = 1`` (Mandatory)
* ``Type = mp``
* ``Recipient.PhoneNumber`` must be set with a +4511223344 format

The response is the order, including a userInputUrl, that can be handled by the salesperson.



