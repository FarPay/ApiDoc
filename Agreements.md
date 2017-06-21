# Agreements
The agreemnets endpoint give you access to all recurring payment instruments, 
that your customers have aquired. Use case cenarios are:
* Get all agreements
* Get a single agreement
* Create an agreement
* Cancel an agreement

**Remark!** that [all requests must have](All-Requests.md) an `X-API-KEY`, and a `Accept` mentioned in the hearder requests. 

And further more, when creating payment instruments, *bank account*-based reccurring payment instruments (*Betalingsservice* and *Leverandørservice*) can be created with the API, while the card must be created in a secure PCI approved environment, which are [available to the customer with FarPay](Customer-Create-PaymentInstruments-By-Email.md) 

# Get all agreements
Getting all agreements, will give you a total view of your customer's payment instruments.
The endpoint is available as `HTTP_GET` from `https://api.farpay.io/v2/agreements`

The result is a collection of agreementes, example below of a card, where the card info is placed in the details.
````Javsacript
[
  {
    "Id": 0,
    "Type": "Card",
    "Status": "Active",
    "CustomerNumber": "12345",
    "PayerID": "",
    "Details": "Card|MasterCard|4444xxxxxxxx2345|04/20",
    "StartDate": "2017-06-20T23:24:36.143Z",
    "ExpireDate": ""
  }
]
````
Here is how the different recurring payment instruments are presented:

 .  | Type | Status | PayerID |Details | StartDate | ExpireDate
----|------|--------|---------|--------|-----------|------------   
Leverandørservice | LS | `Queue`, `Active`, `Passive`, `Error` | CVR number | bank account number if available | start date | has no exire date, but will be terminated on request 
Betalingsservice | BS | `Queue`, `Active`, `Passive`, `Error` | CPR number |  bank account number if available | start date | has no exire date, but will be terminated on request 
Card | Card | `Queue`, `Active`, `Passive`, `Error` | no requirements | Cardtype ( `Visa`, `MasterCard` or `Dankort`), the the cardmask: 4444xxxxxxxx2345 and finally the expire year/month | start date | expire date

# Get a single agreemente
Get a single agreement by adding the `HTTP_GET` to the endpoint `https://api.farpay.io/agreement/{id}`, where the `id` contains a numeric value. The result is the same as getting the collection of agreements, mentioned above.

# Create an agreement
The agreement, can be a based on Leverandørservice (`LS`) or a Betalingsservice (`BS`) payment instrument.
When createing the bank information is given, and must be aligned with the right owner, which is identified by `CVR`-number or a `CPR`-number.

Here is an example of creating an Betalingsservice agreement:

```Javascript
{
  "BankRegNumber": "1234",
  "BankAccountNumber": "12345678",
  "Type": "BS",
  "CustomerNumber": "332211",
  "PayerID": "12345678"
}
```

    | BankRegNumber | BankAccountNumber | Type | PayerID  
----|---------------|-------------------|------|---------
Betalingsservice | `four digits` | `seven` to `eight` digits | `BS` | Danish CPR or CVR number
Leverandørservice | `four digits` | `seven` to `eight` digits | `LS` | Danish CVR number

**Remark!** We have to emphasis on the relation between the account registration and the `PayerID` registration. The `PayerID` identifies the owner of the account, and will be evaluated by the finansial institution, and rejected when no match is found.
And further more, Betalingsservice can hold a business account, as well as a private account. 
