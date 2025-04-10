Navigation: [Customers](../Readme.md) / [Customer](Readme.md) /  Agreement Request

# Agreement request
Give the customer the ability to create an agreement. There are two distribution methods:
* Email
* SMS

## Email request
Send an e-mail to customer `123456` with email address `hans@hansen.dk`

```
    https://farpay-api-staging.azurewebsites.net/v2/customers/123456/agreementRequest?type=card&email=hans%40hansen.dk
```



## SMS Request
Send an SMS to customer `123456` with phone number `+45nnnnnnnn`

```
    https://farpay-api-staging.azurewebsites.net/v2/customers/123456/agreementRequest?type=card&phone=%2B45nnnnnnnn
```
