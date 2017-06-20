# ApiDoc
Vores API er nu tilgængeligt over Swagger, et dokumentations og test framework til API. Dette er gjort for at udviklere hurtigt kan komme igang med at bruge og teste APIet, og for at orienteringen omkring udviklingen bliver fokuseret på ét sted, nemlig i vores Swagger dokumentation.

Naviger til : https://api.farpay.io/swagger

Om du har spørgsål omkring vores gamle API, kan du finde det [her](README-Legacy.md).

## Authentikering
For at bruge API, skal du bruge et token, som skal lægges i hver forespørgsl, der sendes til API. 
Nøglen placeres i headeren under navnet: X-API-KEY. Dette kan du rekviere ved at prøve FarPay i 14 dage eller at ved at blive vores kunde. Information omkring vores priser ses på vores hjemmeside www.farpay.io.

# Programdokumentation
Program dokumentationen bliver løbende opdateret sammen med API'et, og findes på: https://api-farpay.azurewebsites.net/help

# Begreber
APIet er drevet af forretningsbegreber, der udstedes på en forståelig måde igennem vores API dokumentation. Begreberne er noteret i det engelske sprog.

## Begrebsliste
* [Customers](https://api.farpay.io/swagger/ui/index#/Customers) (Kunder)
* [Agreements](https://api.farpay.io/swagger/ui/index#/Agreements) (Aftaler)
* [Invoices](https://api.farpay.io/swagger/ui/index#/Invoices) (Fakturaer)
* [Payments](https://api.farpay.io/swagger/ui/index#/Payments) (Betalinger)
* [Subscriptions](https://api.farpay.io/swagger/ui/index#/Subscriptions) (Abonnementer)

## Om Swagger
Lidt læsning om [Swagger](http://swagger.io/docs/specification/what-is-swagger/)
