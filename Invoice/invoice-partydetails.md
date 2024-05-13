# Invoice PartyInfo Details

*These changes were introduced: May 2024.*

This document showcases enhancements aimed at enriching invoice data.

With these improvements, FarPay customers utilizing the API for invoice creation, now have the capability to include additional Party Info details relevant to the invoice. These enhancements have been implemented and are currently in production, ensuring a more comprehensive invoicing experience for users.

## Types of Party Infos
There are 4 types of Party Infos associated with an Invoice.

- Seller Party
- Recipient Party
- Buyer Party
- Destination Party

#### Seller Party
The *seller party* consistently refers to the company issuing the invoice. Information pertaining to the Seller Party is always present and remains static, as it does not require modification upon invoice creation.

#### Recepient Party
The *recepient party* serves as the recipient of the invoice and can be designated during the creation of an invoice via the FarPay API.

#### Buyer Party (Optional)
The *buyer party* section is optional and allows for specifying information about the buyer separately from the recipient. This enables differentiation in scenarios where the buyer and recipient are distinct entities.

#### Destination Party (Optional)
The *destination party* becomes relevant if the invoice includes details regarding the destination of goods, or services, how they should be delivered and such.

### An Example

**Company A** is a conglomerate comprising multiple subsidiaries, one of which is **Company B**. **Company B** oversees the procurement of office supplies across its various branches. When it comes to purchasing office furniture, **Company B** relies on **Company C** as its supplier.

#### Populating Party Infos:
* Seller Party (Company C): 
    * The seller party information remains static and is populated with Company C's details, including its name, address, and contact information. This information is used consistently on all invoices issued by Company C.
* Recipient Party (Company A):
    * As the recipient of the invoice, the recepient party information is Company A's details. This includes Company A's name, address, and contact information. This information is typically predefined in the invoicing system.
* Buyer Party (Company B):
    * Since Company B is the subsidiary purchasing the office furniture, the buyer party information pertains to Company B's details. This includes Company B's name, address, and contact information. This information allows Company A to easily identify that the purchase was made by Company B, a subsidiary of Company A.
* Destination Party (Company B's Branch):
    *  The destination party information specifies where the goods or services are being delivered. It may pertain to a branch of either Company B or Company A. For instance, if the office furniture is destined for Company B's branch in New York, the destination party information would include the address and contact details of Company B's New York branch.

#### Invoice Scenario:
When **Company B** purchases office furniture from **Company C**, the invoice is addressed to **Company A**, the parent company, as per the recepient party information. However, the invoice indicates that the purchase was made by **Company B**, as specified in the buyer party information. If the office furniture is intended for a specific branch of **Company B**, such as the New York branch, then the destination party information would reflect this branch's details.

In summary, the seller party remains constant **(Company C)**, the recepient party is the parent company **(Company A)**, the buyer party identifies the subsidiary making the purchase **(Company B)**, and the destination party specifies the branch or location receiving the goods (if applicable). This structured approach to party information ensures clarity and accuracy in invoicing processes, particularly in complex business structures involving multiple entities.

## Enriching the invoice with party info details.

The main documentation regarding creating invoice can be seen [***here***](Invoice.md)

The following JSON shows an example of how the Recipient, Buyer and Destination could be populated when inserting an Invoice.

```json
{
...
  "Recipient": {
    "CustomerNumber": "12345678",
    "CompanyNo": "98765432",
    "Gln": "1234567890123",
    "Name": "Company A - Copenhagen Office",
    "Email": "info@companyA.com",
    "Street": "456 City Center Avenue",
    "PostCode": "1234",
    "PoBox": "PO Box 123",
    "City": "Copenhagen",
    "Country": "DK",
    "ContactId": "Cust123",
    "ContactName": "John Doe",
    "ContactPhone": "+4523456789",
    "ContactEmail": "john.doe@companyA.com"
  },
  "Buyer": {
    "CompanyNo": "87654321",
    "Gln": "9876543210987",
    "Name": "Company B - London Office",
    "Street": "789 Business District Road",
    "PostCode": "SW1A 1AA",
    "City": "London",
    "Country": "UK",
    "ContactInformation": {
      "Identifier": "Buyer456",
      "Name": "Jane Smith",
      "Phone": "+1987654321",
      "Email": "jane.smith@companyB.com",
      "Role": "Purchasing Manager"
    }
  },
  "Destination": {
    "CompanyNo": "13579246",
    "Gln": "5432167890123",
    "Name": "Company B - New York Branch",
    "Street": "123 Broadway",
    "PostCode": "10007",
    "City": "New York",
    "Country": "US",
    "ContactInformation": {
      "Identifier": "Branch789",
      "Name": "Michael Johnson",
      "Phone": "+1765432198",
      "Email": "michael.johnson@branchXYZ.com",
      "Role": "Branch Manager"
    }
  }
...
}
```

## Summary
These changes to the API Endpoint introduce enhancements to accommodate the designation of the *Buyer-* and *Destination* Party.

* Recipient:
    * The recipient section now includes three new optional properties: ContactId, ContactPhone, and ContactEmail, providing additional flexibility in specifying contact details.
* Buyer (Optional):
    * An optional object allows for specifying information about the buyer separately from the recipient, enabling differentiation in scenarios where the buyer and recipient are distinct entities.
* Destination (Optional):
    * Another optional object, *Destination*, facilitates the designation of the party to whom the goods or services are intended. This provides clarity in scenarios where the recipient may not be the final destination of the goods or services.

These adjustments signify a significant step forward in improving the flexibility and precision of the API endpoint. By allowing for more granular control over invoice details, FarPay is committed to delivering a more tailored and efficient invoicing experience for its users. As we continue to refine and enhance our services, feedback and suggestions from our valued customers are invaluable in driving further improvements.
