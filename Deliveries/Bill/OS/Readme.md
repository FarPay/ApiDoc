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
                        <PaymentIdentifier>
                            ...details...
                        </PaymentIdentifier>                            
                    </FarPay>
                </ExtensibleContent>
            </PaymentMeans>
        </Bill>
    </Bills>
</FarPayXml>
```

## Payout details
Overførselsservice has following schemas for the payout details:

| Schema | Description                                                                                                              | Code example                                                                    |
|--------|--------------------------------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------|
| `Bank` | The bank account details are set with<br/><ul><li>Bank registration number `rrrr`</li><li>Bank account number `aaaaaaaa`</li></ul> | ```<PaymentIdenitifyer scheme="Bank">rrrr:aaaaaaaa</PaymentIdentifyer>```       | 
| `CVR`  | The CVR number of the receiver                                                                                           | ```<PaymentIdenitifyer scheme="CVR">12345678</PaymentIdentifyer>```             |
| `CPR`  | The CPR number of the receiver                                                                                           | ```<PaymentIdenitifyer scheme="CPR">0102889999</PaymentIdentifyer>``` |



* CVR
* CPR
* BANK
* 