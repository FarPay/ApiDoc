Navigate: [API Doc](../../../Readme.md) / [Deliveries](../../Readme.md) / [Extensions](../Readme.md) / [Examples](Readme.md) / Force send

# Force send method
For merchants, that have a configuration of automatically sending an e-mail or XML document to the customer, 
FarPay facilitates an alternative method of sending the document, that is enforced over the default convention.

This is done by setting the `DeliveryMethod` in the XML document. Available properties are:
* `Default`
* `Print` (Force to send to print)
* `PrintExpress` (Sent directly to print provider, with extra charge)


