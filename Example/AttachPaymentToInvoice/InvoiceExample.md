# Invoice example.

To delivery an invoice, that is to be attached to a payment, you will need to create an OIO Ubl invoice object.
In addition to the standard OIO Ubl invoice, you will need to add a `FarPay` extension, that contains the `OrderToken`

The example below shows the token: ``1qaz2wsx3edc4rfv5tgdfvdsrg`` embedded with the amount:


```XML
<UBLExtensions xmlns="urn:oasis:names:specification:ubl:schema:xsd:CommonExtensionComponents-2">
    <UBLExtension>
        <ID xmlns="urn:oasis:names:specification:ubl:schema:xsd:CommonBasicComponents-2">FarPay</ID>
        <ExtensionContent>
            <FarPay>
                <CaptureAmount>99.00</CaptureAmount>
                <OrderToken>1qaz2wsx3edc4rfv5tgdfvdsrg</OrderToken>
            </FarPay>
        </ExtensionContent>
    </UBLExtension>
</UBLExtensions>

```

Now the extension is added to the invoice document, as shown below:

```xml
<?xml version="1.0" encoding="utf-8"?>
<Invoice xmlns:xsd="http://www.w3.org/2001/XMLSchema"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xmlns="urn:oasis:names:specification:ubl:schema:xsd:Invoice-2">
    <UBLExtensions xmlns="urn:oasis:names:specification:ubl:schema:xsd:CommonExtensionComponents-2">
        <UBLExtension>
            <ID xmlns="urn:oasis:names:specification:ubl:schema:xsd:CommonBasicComponents-2">FarPay</ID>
            <ExtensionContent>
                <FarPay>
                    <CaptureAmount>99.00</CaptureAmount>
                    <OrderToken>1qaz2wsx3edc4rfv5tgdfvdsrg</OrderToken>
                </FarPay>
            </ExtensionContent>
        </UBLExtension>
    </UBLExtensions>
    <UBLVersionID xmlns="urn:oasis:names:specification:ubl:schema:xsd:CommonBasicComponents-2">2.0</UBLVersionID>
    <CustomizationID xmlns="urn:oasis:names:specification:ubl:schema:xsd:CommonBasicComponents-2">OIOUBL-2.01</CustomizationID>
    <ProfileID schemeID="urn:oioubl:id:profileid-1.2" schemeAgencyID="320"
        xmlns="urn:oasis:names:specification:ubl:schema:xsd:CommonBasicComponents-2">urn:www.nesubl.eu:profiles:profile5:ver2.0</ProfileID>
    <ID xmlns="urn:oasis:names:specification:ubl:schema:xsd:CommonBasicComponents-2">187505511</ID>
    <IssueDate xmlns="urn:oasis:names:specification:ubl:schema:xsd:CommonBasicComponents-2">2025-05-05</IssueDate>
    <InvoiceTypeCode listID="urn:oioubl:codelist:invoicetypecode-1.1" listAgencyID="320"
        xmlns="urn:oasis:names:specification:ubl:schema:xsd:CommonBasicComponents-2">380</InvoiceTypeCode>
    <DocumentCurrencyCode xmlns="urn:oasis:names:specification:ubl:schema:xsd:CommonBasicComponents-2">DKK</DocumentCurrencyCode>
    <AccountingSupplierParty xmlns="urn:oasis:names:specification:ubl:schema:xsd:CommonAggregateComponents-2">
        <Party>
            <EndpointID schemeID="DK:CVR"
                xmlns="urn:oasis:names:specification:ubl:schema:xsd:CommonBasicComponents-2">DK11111111</EndpointID>
            <PartyName>
                <Name xmlns="urn:oasis:names:specification:ubl:schema:xsd:CommonBasicComponents-2">MINVIRKSOMHED</Name>
            </PartyName>
            <PostalAddress>
                <AddressFormatCode listID="urn:oioubl:codelist:addressformatcode-1.1" listAgencyID="320"
                    xmlns="urn:oasis:names:specification:ubl:schema:xsd:CommonBasicComponents-2">StructuredDK</AddressFormatCode>
                <StreetName xmlns="urn:oasis:names:specification:ubl:schema:xsd:CommonBasicComponents-2">Rådhuspladsen</StreetName>
                <BuildingNumber xmlns="urn:oasis:names:specification:ubl:schema:xsd:CommonBasicComponents-2">3</BuildingNumber>
                <CityName xmlns="urn:oasis:names:specification:ubl:schema:xsd:CommonBasicComponents-2">København K</CityName>
                <PostalZone xmlns="urn:oasis:names:specification:ubl:schema:xsd:CommonBasicComponents-2">1147</PostalZone>
                <Country>
                    <IdentificationCode xmlns="urn:oasis:names:specification:ubl:schema:xsd:CommonBasicComponents-2">DK</IdentificationCode>
                </Country>
            </PostalAddress>
            <PartyLegalEntity>
                <CompanyID schemeID="DK:CVR"
                    xmlns="urn:oasis:names:specification:ubl:schema:xsd:CommonBasicComponents-2">DK11111111</CompanyID>
            </PartyLegalEntity>
        </Party>
    </AccountingSupplierParty>
    <AccountingCustomerParty xmlns="urn:oasis:names:specification:ubl:schema:xsd:CommonAggregateComponents-2">
        <AdditionalAccountID schemeID="CustomerNumber"
            xmlns="urn:oasis:names:specification:ubl:schema:xsd:CommonBasicComponents-2">112233445566</AdditionalAccountID>
        <AdditionalAccountID schemeID="AccountNumber"
            xmlns="urn:oasis:names:specification:ubl:schema:xsd:CommonBasicComponents-2">1122336644</AdditionalAccountID>
        <Party>
            <EndpointID schemeID="GLN"
                xmlns="urn:oasis:names:specification:ubl:schema:xsd:CommonBasicComponents-2">0000000000000</EndpointID>
            <PartyIdentification>
                <ID schemeID="DK:CVR"
                    xmlns="urn:oasis:names:specification:ubl:schema:xsd:CommonBasicComponents-2">DK00000000</ID>
            </PartyIdentification>
            <PartyName>
                <Name xmlns="urn:oasis:names:specification:ubl:schema:xsd:CommonBasicComponents-2"></Name>
            </PartyName>
            <PostalAddress>
                <AddressFormatCode listID="urn:oioubl:codelist:addressformatcode-1.1" listAgencyID="320"
                    xmlns="urn:oasis:names:specification:ubl:schema:xsd:CommonBasicComponents-2">StructuredDK</AddressFormatCode>
                <StreetName xmlns="urn:oasis:names:specification:ubl:schema:xsd:CommonBasicComponents-2">receiver@company.inc</StreetName>
                <BuildingNumber xmlns="urn:oasis:names:specification:ubl:schema:xsd:CommonBasicComponents-2">-</BuildingNumber>
                <PostalZone xmlns="urn:oasis:names:specification:ubl:schema:xsd:CommonBasicComponents-2">-</PostalZone>
                <Country>
                    <IdentificationCode xmlns="urn:oasis:names:specification:ubl:schema:xsd:CommonBasicComponents-2">DK</IdentificationCode>
                </Country>
            </PostalAddress>
            <PartyLegalEntity>
                <CompanyID schemeID="DK:CVR"
                    xmlns="urn:oasis:names:specification:ubl:schema:xsd:CommonBasicComponents-2">DK00000000</CompanyID>
            </PartyLegalEntity>
            <Contact>
                <ID xmlns="urn:oasis:names:specification:ubl:schema:xsd:CommonBasicComponents-2">-</ID>
                <ElectronicMail xmlns="urn:oasis:names:specification:ubl:schema:xsd:CommonBasicComponents-2">receiver@company.inc</ElectronicMail>
                <Note xmlns="urn:oasis:names:specification:ubl:schema:xsd:CommonBasicComponents-2">new note</Note>
            </Contact>
        </Party>
    </AccountingCustomerParty>
    <PaymentMeans xmlns="urn:oasis:names:specification:ubl:schema:xsd:CommonAggregateComponents-2">
        <ID xmlns="urn:oasis:names:specification:ubl:schema:xsd:CommonBasicComponents-2">888887888</ID>
        <PaymentMeansCode xmlns="urn:oasis:names:specification:ubl:schema:xsd:CommonBasicComponents-2">93</PaymentMeansCode>
        <PaymentDueDate xmlns="urn:oasis:names:specification:ubl:schema:xsd:CommonBasicComponents-2">2025-05-05</PaymentDueDate>
        <PaymentChannelCode listID="urn:oioubl:codelist:paymentchannelcode-1.1"
            xmlns="urn:oasis:names:specification:ubl:schema:xsd:CommonBasicComponents-2">DK:FIK</PaymentChannelCode>
        <InstructionID xmlns="urn:oasis:names:specification:ubl:schema:xsd:CommonBasicComponents-2">000000000111111</InstructionID>
        <PaymentID xmlns="urn:oasis:names:specification:ubl:schema:xsd:CommonBasicComponents-2">71</PaymentID>
        <CreditAccount>
            <AccountID xmlns="urn:oasis:names:specification:ubl:schema:xsd:CommonBasicComponents-2">88888888</AccountID>
        </CreditAccount>
    </PaymentMeans>
    <TaxTotal xmlns="urn:oasis:names:specification:ubl:schema:xsd:CommonAggregateComponents-2">
        <TaxAmount currencyID="DKK"
            xmlns="urn:oasis:names:specification:ubl:schema:xsd:CommonBasicComponents-2">0.00</TaxAmount>
        <TaxSubtotal>
            <TaxableAmount currencyID="DKK"
                xmlns="urn:oasis:names:specification:ubl:schema:xsd:CommonBasicComponents-2">99.00</TaxableAmount>
            <TaxAmount currencyID="DKK"
                xmlns="urn:oasis:names:specification:ubl:schema:xsd:CommonBasicComponents-2">0.00</TaxAmount>
            <TaxCategory>
                <ID schemeID="urn:oioubl:id:taxcategoryid-1.1" schemeAgencyID="320"
                    xmlns="urn:oasis:names:specification:ubl:schema:xsd:CommonBasicComponents-2">ZeroRated</ID>
                <Percent xmlns="urn:oasis:names:specification:ubl:schema:xsd:CommonBasicComponents-2">0.00</Percent>
                <TaxScheme>
                    <ID schemeID="urn:oioubl:id:taxschemeid-1.1" schemeAgencyID="320"
                        xmlns="urn:oasis:names:specification:ubl:schema:xsd:CommonBasicComponents-2">63</ID>
                    <Name xmlns="urn:oasis:names:specification:ubl:schema:xsd:CommonBasicComponents-2">Moms</Name>
                </TaxScheme>
            </TaxCategory>
        </TaxSubtotal>
    </TaxTotal>
    <LegalMonetaryTotal xmlns="urn:oasis:names:specification:ubl:schema:xsd:CommonAggregateComponents-2">
        <LineExtensionAmount currencyID="DKK"
            xmlns="urn:oasis:names:specification:ubl:schema:xsd:CommonBasicComponents-2">99.00</LineExtensionAmount>
        <TaxExclusiveAmount currencyID="DKK"
            xmlns="urn:oasis:names:specification:ubl:schema:xsd:CommonBasicComponents-2">0.00</TaxExclusiveAmount>
        <TaxInclusiveAmount currencyID="DKK"
            xmlns="urn:oasis:names:specification:ubl:schema:xsd:CommonBasicComponents-2">99.00</TaxInclusiveAmount>
        <PayableAmount currencyID="DKK"
            xmlns="urn:oasis:names:specification:ubl:schema:xsd:CommonBasicComponents-2">99.00</PayableAmount>
    </LegalMonetaryTotal>
    <InvoiceLine xmlns="urn:oasis:names:specification:ubl:schema:xsd:CommonAggregateComponents-2">
        <ID xmlns="urn:oasis:names:specification:ubl:schema:xsd:CommonBasicComponents-2">1</ID>
        <InvoicedQuantity unitCode="EA"
            xmlns="urn:oasis:names:specification:ubl:schema:xsd:CommonBasicComponents-2">1</InvoicedQuantity>
        <LineExtensionAmount currencyID="DKK"
            xmlns="urn:oasis:names:specification:ubl:schema:xsd:CommonBasicComponents-2">99.00</LineExtensionAmount>
        <Delivery>
            <RequestedDeliveryPeriod>
                <StartDate xmlns="urn:oasis:names:specification:ubl:schema:xsd:CommonBasicComponents-2">2025-05-05</StartDate>
                <EndDate xmlns="urn:oasis:names:specification:ubl:schema:xsd:CommonBasicComponents-2">2025-06-04</EndDate>
                <Description xmlns="urn:oasis:names:specification:ubl:schema:xsd:CommonBasicComponents-2">Produkt 1</Description>
            </RequestedDeliveryPeriod>
            <DeliveryParty>
                <PartyName>
                    <Name xmlns="urn:oasis:names:specification:ubl:schema:xsd:CommonBasicComponents-2">-</Name>
                </PartyName>
                <PostalAddress>
                    <AddressFormatCode listID="urn:oioubl:codelist:addressformatcode-1.1" listAgencyID="320"
                        xmlns="urn:oasis:names:specification:ubl:schema:xsd:CommonBasicComponents-2">StructuredDK</AddressFormatCode>
                    <StreetName xmlns="urn:oasis:names:specification:ubl:schema:xsd:CommonBasicComponents-2">-</StreetName>
                    <BuildingNumber xmlns="urn:oasis:names:specification:ubl:schema:xsd:CommonBasicComponents-2">-</BuildingNumber>
                    <MarkCare xmlns="urn:oasis:names:specification:ubl:schema:xsd:CommonBasicComponents-2">-</MarkCare>
                    <PostalZone xmlns="urn:oasis:names:specification:ubl:schema:xsd:CommonBasicComponents-2">-</PostalZone>
                </PostalAddress>
                <Contact>
                    <ElectronicMail xmlns="urn:oasis:names:specification:ubl:schema:xsd:CommonBasicComponents-2">-</ElectronicMail>
                </Contact>
            </DeliveryParty>
        </Delivery>
        <TaxTotal>
            <TaxAmount currencyID="DKK"
                xmlns="urn:oasis:names:specification:ubl:schema:xsd:CommonBasicComponents-2">0.00</TaxAmount>
            <TaxSubtotal>
                <TaxableAmount currencyID="DKK"
                    xmlns="urn:oasis:names:specification:ubl:schema:xsd:CommonBasicComponents-2">99.00</TaxableAmount>
                <TaxAmount currencyID="DKK"
                    xmlns="urn:oasis:names:specification:ubl:schema:xsd:CommonBasicComponents-2">0.00</TaxAmount>
                <TaxCategory>
                    <ID schemeID="urn:oioubl:id:taxcategoryid-1.1" schemeAgencyID="320"
                        xmlns="urn:oasis:names:specification:ubl:schema:xsd:CommonBasicComponents-2">ZeroRated</ID>
                    <Percent xmlns="urn:oasis:names:specification:ubl:schema:xsd:CommonBasicComponents-2">0.00</Percent>
                    <TaxScheme>
                        <ID schemeID="urn:oioubl:id:taxschemeid-1.1" schemeAgencyID="320"
                            xmlns="urn:oasis:names:specification:ubl:schema:xsd:CommonBasicComponents-2">63</ID>
                        <Name xmlns="urn:oasis:names:specification:ubl:schema:xsd:CommonBasicComponents-2">Moms</Name>
                    </TaxScheme>
                </TaxCategory>
            </TaxSubtotal>
        </TaxTotal>
        <Item>
            <Description xmlns="urn:oasis:names:specification:ubl:schema:xsd:CommonBasicComponents-2">Produkt 2</Description>
            <Name xmlns="urn:oasis:names:specification:ubl:schema:xsd:CommonBasicComponents-2">N/A</Name>
            <AdditionalInformation xmlns="urn:oasis:names:specification:ubl:schema:xsd:CommonBasicComponents-2">WEA</AdditionalInformation>
            <SellersItemIdentification>
                <ID xmlns="urn:oasis:names:specification:ubl:schema:xsd:CommonBasicComponents-2">123456789</ID>
            </SellersItemIdentification>
        </Item>
        <Price>
            <PriceAmount currencyID="DKK"
                xmlns="urn:oasis:names:specification:ubl:schema:xsd:CommonBasicComponents-2">99.00</PriceAmount>
            <BaseQuantity unitCode="EA"
                xmlns="urn:oasis:names:specification:ubl:schema:xsd:CommonBasicComponents-2">1</BaseQuantity>
        </Price>
    </InvoiceLine>
</Invoice>
```
