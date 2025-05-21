Breadcrumbs: [Deliveries](?d=Deliveries) / [Bill](?d=Deliveries/Bill) 


# Bill

The bill format is a business-driven format, with the lowest common denominator of of receiving a bill 
supplmeneted with an instruction of how the bill is to be paid or payout.

The bill format can both hold a single bill, or a bulk of bills. 
The format is an XML-Format, that is *only used* in the FarPay system.

## Requirements
| Requirement          | Description                                                                                              |
|----------------------|----------------------------------------------------------------------------------------------------------|
| `X-API-KEY`          | Merchant API key, aquired from the FarPay settings page.                                                 |
| Document body        | The document is expresed as a standard bill. This document will express the requirements to the document | 


## Bill format XSD
The bill format-authority is placed in an XSD document, available from:

```
    https://app.farpay.io/xsd/bills/bills.xsd
```

## Instructions
When creating a bill, you need to create a delivery, that is wrapping the actual bill or bills.
Bear in mind, that the bill format needs to be transformed into a base64 format, that is decoded into the XML, that
is processed in FarPay.

## Steps when creating a Bill

<ol>
    <li>Get the XSD document, and create a bill file.</li>
    <li>Encode the attached PDF-document into a base64 format, and hold the document for later use</li>
    <li>Put the base64 string into the <code>EncodedDocument</code> container.</li>
    <li>Convert the howl XML document into a base64 string (including the <code>EncodedDocument</code>.</li>
    <li>Create a Delivery form the delivery endpoint with following data:</li>
    <ol>
        <li><code>DeliveryType</code> = <code>Bill</code></li>
        <li><code>DeliveryFormat</code> = <code>XML</code></li>
        <li>The <code>File</code></li>
        <ol>
            <li>The <code>Filename</code></li>
            <li>The <code>Data</code></li>
        </ol>
    </ol>
    <li>Where you Put the base64 string (of the <code>Bill</code>-format) into the <code>File</code> tag of <code>Delivery</code>.</li>
    <li>POST the request</li>
</ol>

### Example of how to produce a bill

First you need the attached PDF, and convert it into a base64 format. This is not part of the FarPay system.
And give that you have the PDF in a base64 format, you can use the following code to create a bill.

Example of a base64:
```javascript
    JVBERi0xLjcNCiW1t......olJUVPRg==
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
            <InvoiceNumber>CRED-12345</InvoiceNumber>
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
        </Bill>
    </Bills>
</FarPayXml>
```

This XML document is then converted into a base64 format,

```
PD94bWwgdmVyc2lvbj0iMS4wIiBlbm......+DQo8L0ZhclBheVhtbD4=
```

This is the final base64 format, and put into the `File` tag of the delivery.

``POST https://api.farpay.io/v2/deliveries``

With body:
```javascript
{
  "DeliveryType": "Bill",
  "DeliveryFormat": "XML",
  "File": {
    "Filename": "MyFile.xml",
    "Data": "PD94bWwgdmVyc2lvbj0iMS4wIiBlbm......+DQo8L0ZhclBheVhtbD4="
  }
}
```
### Result
Now the delivery is created, with the attached file. The processing of the file will occur in the background, 
and result can be checked at the deliveries endpoint: ``https://api.farpay.io/v2/deliveries/<delivery ID>``
Where the `<delivery ID>` is the ID of the delivery you just created.

