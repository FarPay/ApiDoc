# [ApiDoc](../../../README.md) / [Invoices](../../Invoices.md) / [Invoice](../Invoice.md) / Invoice Refund

-----------------

# Invoice Refund

When an invoice paid, a refund event can be triggered. This document describes the refund event, 
and how it is handled in FarPay.

There are some limits to how a refund can be handled. The refund can only be handled, if the invoice is paid,
and the payment is eligable for a refund. The refund can be handled in two ways:
    1. The refund is handled by the creditor, and the refund is transfered to the debtor
    2. The refund is handled by the creditor, and the refund is transfered to the creditor