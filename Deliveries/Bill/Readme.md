Breadcrumbs: [Deliveries](?d=Deliveries) / [Bill](?d=Deliveries/Bill) 


# Bill

The bill format is a business-driven format, with the lowest common denominator of of receiving a bill 
supplmeneted with an instruction of how the bill is to be paid or payout.

The bill format can both hold a single bill, or a bulk of bills. 
The format is an XML-Format, that is *only used* in the FarPay system.

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

