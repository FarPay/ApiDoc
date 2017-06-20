# ApiDoc
Vores API er nu tilgængeligt over Swagger, et dokumentations og test framework til API. Dette er gjort for at udviklere hurtigt kan komme igang med at bruge og teste APIet, og for at orienteringen omkring udviklingen bliver fokuseret på ét sted, nemlig i vores Swagger dokumentation.

Naviger til : https://api.farpay.io/swagger - og læs lidt om [swagger](http://swagger.io/docs/specification/what-is-swagger/)

Om du har spørgsål omkring vores gamle API, kan du finde det [her](README-Legacy.md).

## Prøv gratis
For at prøve FarPay gratis, kan du igennem https://www.farpay.io/dk/?showtrial=true og efterfølgende bruge vores chatt at få tilsendt en API nøgle.

Vores api er bygget omkring følgende konvension:
* Endepunkterne er versioneret, og har dette som en del af referencen.
   * Nuværende version er `v2`
   * Url er derfor: `https://api.farpay.io/v2`
* Alle endepunkter autentikeres med en [API-nøgle](Get-Api-Key.md)
* Alle endepunkter har en HTTP_GET, der returnerer en kollektion af disse. F.eks. en kollektion af kunder.
* Alle endepunkter har en HTTP_GET, der ligger under endepunkted med reference af en enkelt instans, f.eks. /customers/2, der returnerer kunde med kundenummer 2.
* Ud over disse, konventioner optræder variation over hvad man kan for hvert endepunkt. Disse er beskrevet under program dokumentationen og i links for de forskellige endepunkter.

Betragt swagger dokumenationen for *hvordan* et kald foretages, og *program dokumentationen* som vejledning for hvorfor kaldet foretages.

# Begreber
APIet er drevet af forretningsbegreber, der udstedes på en forståelig måde igennem vores API dokumentation. Begreberne er noteret i det engelske sprog.

## Begrebsliste (links til Swagger)
* [Customers](https://api.farpay.io/swagger/ui/index#/Customers) (Kunder)
* [Agreements](https://api.farpay.io/swagger/ui/index#/Agreements) (Aftaler)
* [Invoices](https://api.farpay.io/swagger/ui/index#/Invoices) (Fakturaer)
* [Payments](https://api.farpay.io/swagger/ui/index#/Payments) (Betalinger)
* [Subscriptions](https://api.farpay.io/swagger/ui/index#/Subscriptions) (Abonnementer)

# Program dokumentation
Ud fra nævnte begreber, bliver hvert begreb, beskrevet med nødvendige dokumentationsteknikker, for at belyse hvorledes du med API kan se og ændre de tilstande disse begreber kan havne i.

## Kunder  (Customers)
Med en liste af kunder `https://api.farpay.io/v2/customers` hvor der returneres en lista af `CustomerReference` (kunde referencer), som indholder [basis informationer omkring kunden](CustomerReference.md).
Til at få et [fuldstændigt billede af kunden](Customer.md), og den aktive betalingsaftle, som kunden har skal endepunktet `https://api.farpay.io/v2/customerse/<kundenummer>` bruges. 
