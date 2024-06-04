# Opret kunde

Når en kunde oprettes gennem API i FarPay, angives basis oplysningerne for kunden.
Om FarPay kører i integreret tilstand, bliver stam oplysningerne omkring kunden hentet fra regnskabs systemet.
Kunden, som bliver oprette i API bliver ikke synkroniseret ind i dit regnskabssystem, men overskrevet når det samme kundenummer bliver oprettet i regnskabssystemet.

```c#

var test = "1";

```
