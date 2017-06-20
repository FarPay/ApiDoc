# ApiDoc

For at bruge vores API, skal du bruge et clientId og en clientSecret. Dette kan du rekviere ved at prøve FarPay i 14 dage eller at ved at blive vores kunde. Information omkring vores priser ses på vores hjemmeside www.farpay.io.

# Programdokumentation
Program dokumentationen bliver løbende opdateret sammen med API'et, og findes på: https://api-farpay.azurewebsites.net/help

# Begreber
I API arbejder vi med forståelige begreber, der efter behov bliver udviklet.

## Begrebsliste
* Invoice
* Customer
* Agreement
* Payment 

# Eksempler
Med disse eksempler får du udbygget dit faktura flow med de tilgængelige betalings instrumenter (Betalingsservice, Leverandørservice, MobilePay Invoice og FI). Eksemplerne er delt op i følgende sektioner:
* Kunder 
* Fakturaer
* Betalinger

## Kunder
Kunde kartoteket - stamoplysningerne - bliver synkroniseret fra dir regnskabssystem om du kører FarPay som integration. Kunde oplysninger, som bliver oprettet i FarPay alene bliver ikke synkroniseret over til dit regnskabssystem.
* [Vis kunder](customerList.md) - Giver en liste af kunder, med kundenummer
* [Opret kunde](customerCreate.md)
* [Vis kunde](customerShow.md) - Viser kunden og evt. tilknyttede betalings instrument(er).

## Fakturaer
* [List fakturaer] (invoiceList.md) - Hent en liste af fakturaer, baseret på kombinerede kriterier
* [Opret faktura](invoiceCreate.md) - Opretter en faktura, baseret på et invoice objekt

## Betalinger
* [Vis betalinger](paymentList.md)
* [Vis betaling](paymentShow.md)
