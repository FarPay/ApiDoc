Breadcrumbs: [Deliveries](?d=Deliveries) / [Bill](?d=Deliveries/Bill) / [OS](?d=Deliveries/Bill/OS) / [Readme](?d=Deliveries/Bill/OS/Readme)

# Overførselsservice
The purpose of the Bill format is to encapsulate the data of a bill, that is to be sent to the receiver.
Further more to express a payout by using a bill, that is compatible with Overførselsservice.

## Requirements
| Requirement          | Description                                                                                              |
|----------------------|----------------------------------------------------------------------------------------------------------|
| `X-API-KEY`          | Merchant API key, aquired from the FarPay settings page.                                                 |
| Document body        | The document is expresed as a standard bill. This document will express the requirements to the document | 

# Bill example

The following XSD document, governs the structure of the Bill XML document.
Remarks that current version of the API only supports bulk insert of the <Bills> tag.

This means that you must create a delivery, without any file content. Hence you will receive a result containing a
LOB storage, that is available for 30 minutes, where you have the capability of pushing the file into that link.


```
    https://app.farpay.io/xsd/bills/bills.xsd
```

```xml
<?xml version="1.0" encoding="UTF-8"?>
<FarPayXml xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
           xsi:schemaLocation="http://app.farpay.io/xsd/bills.xsd">
    <Delivery>
        <Count>1</Count>
    </Delivery>
    <Bills>
        <Bill>
            <InvoiceTypeCode>PCM</InvoiceTypeCode>
            <InvoiceNumber>INV-12345</InvoiceNumber>
            <EncodedDocument>JVBERi0xLjcNCiW1t......olJUVPRg==</EncodedDocument>
            <CustomerNumber>CUST-67890</CustomerNumber>
            <Name>John Doe</Name>
            <Street>Main Street</Street>
            <HouseNumber>42</HouseNumber>
            <PostalZone>12345</PostalZone>
            <CityName>Example City</CityName>
            <Country>CountryName</Country>
            <EmailAddress>johndoe@example.com</EmailAddress>
            <PaymentDueDate>2025-02-01</PaymentDueDate>
            <Currency>DKK</Currency>
            <ToBePayedAmount>123.45</ToBePayedAmount>
            <PaymentMeans>
                <TypeCodeID>BankTransfer</TypeCodeID>
                <PaymentChannelCode>OVERFØRSELSSERVICE</PaymentChannelCode>
                <ExtensibleContent>
                    <FarPay>
                        <PaymentMethod>Payout</PaymentMethod>
                        <Payout>
                            <SenderIdentifier scheme="BANK">rrrr:nnnnnnnn</SenderIdentifier>
                            <ReceiverIdentifier scheme="{BANK | CPR | CVR }"></ReceiverIdentifier>
                        </Payout>                         
                    </FarPay>
                </ExtensibleContent>
            </PaymentMeans>
        </Bill>
    </Bills>
</FarPayXml>
```


## Payout details

Overførselsservice has following schemas for the payout details:

* SenderIdentifier is optional - it should be specificed, if you have mulitple Overførselsservice creditors, otherwise leave blank.
* ReceiverIdentifier, has a scheme identifier, in order to send the money towards the receiver.

| Schema | Description                                                                                                              | Code example                                                                    |
|--------|--------------------------------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------|
| `BANK` | The bank account details are set with<br/><ul><li>Bank registration number `rrrr`</li><li>Bank account number `aaaaaaaa`</li></ul> | ```<PaymentIdenitifyer scheme="Bank">rrrr:aaaaaaaa</PaymentIdentifyer>```       | 
| `CVR`  | The CVR number of the receiver                                                                                           | ```<PaymentIdenitifyer scheme="CVR">12345678</PaymentIdentifyer>```             |
| `CPR`  | The CPR number of the receiver                                                                                           | ```<PaymentIdenitifyer scheme="CPR">0102889999</PaymentIdentifyer>``` |

