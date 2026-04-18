# Maximale Hypotheek Berekener

Een standalone HTML-tool voor een indicatieve berekening van de maximale hypotheek op basis van Nederlandse normen (2025). Geen server nodig — open het bestand gewoon in een browser.

-----

## Gebruik

1. Open `hypotheek-berekener.html` in een webbrowser (Chrome, Firefox, Edge, Safari)
1. Vul je gegevens in — de berekening werkt direct live
1. Je invoer wordt **automatisch opgeslagen** in de browser (localStorage) en hersteld bij de volgende opening
1. Gebruik de knop **↺ Alles wissen** om alle waarden te resetten naar de standaardwaarden

> **Let op:** De opgeslagen waarden zijn gebonden aan de browser én het apparaat waarop je de tool opent. Ze worden niet gesynchroniseerd tussen apparaten.

-----

## Wat wordt berekend

De tool berekent de maximale hypotheek op basis van twee limieten, en neemt de laagste:

### 1. LTI — Loan to Income (inkomensnorm)

Het maximale hypotheekbedrag dat je op basis van je (gezamenlijke) toetsinkomen mag lenen. Gebaseerd op de **NIBUD-financieringslastnormen 2025**, vastgelegd in de *Tijdelijke regeling hypothecair krediet* (Staatsblad van het Koninkrijk der Nederlanden).

De norm loopt op van ~21% (bij laag inkomen) tot ~33% van het bruto jaarinkomen als maximale jaarlast.

### 2. LTV — Loan to Value (woningwaardenorm)

In Nederland mag de hypotheek niet meer bedragen dan **100% van de marktwaarde** van de woning. Kosten koper (~5,5%) moeten uit eigen middelen komen.

### Toetsrente

Bij een rentevaste periode **korter dan 10 jaar** geldt een wettelijke toetsvloer van **5%**, ook als de werkelijke rente lager is. Vanaf 10 jaar wordt getoetst op de werkelijke contractrente.

-----

## Invoervelden

### Situatie

|Veld                       |Toelichting                                                                       |
|---------------------------|----------------------------------------------------------------------------------|
|Starter / Doorstromer      |Doorstromers kunnen overwaarde inbrengen als eigen vermogen                       |
|Verkoopprijs huidige woning|Verwachte opbrengst bij verkoop                                                   |
|Resterende hypotheek       |Openstaande schuld huidige hypotheek — netto overwaarde wordt eigen inbreng       |
|Dubbele woonlasten         |Als je nieuwe woning koopt vóór verkoop huidige: huidige maandlast telt als schuld|

### Inkomen

|Veld                               |Toelichting                                                        |
|-----------------------------------|-------------------------------------------------------------------|
|Bruto jaarinkomen (aanvrager 1 & 2)|Inclusief vakantiegeld (8%); bij vast contract volledig inkomen    |
|Medeaanvrager                      |Beide inkomens worden volledig meegenomen als toetsinkomen         |
|Energielabel A of hoger            |Verhoogde leennorm (~+1% van toetsinkomen) conform regelgeving 2025|

### Lening & rente

|Veld              |Toelichting                                                              |
|------------------|-------------------------------------------------------------------------|
|Rentevaste periode|Bepaalt of toetsvloer van 5% van toepassing is                           |
|Hypotheekrente    |Indicatief; werkelijke rente opvragen bij geldverstrekkers               |
|Looptijd          |Standaard 30 jaar; bij leeftijd >52 realistisch 15–20 jaar (tot AOW/80jr)|
|Type hypotheek    |Annuïtair (vaste last) of Lineair (dalende last)                         |

### Woning & eigen inbreng

|Veld                 |Toelichting                                        |
|---------------------|---------------------------------------------------|
|Marktwaarde / koopsom|Basis voor LTV-berekening                          |
|Extra eigen inbreng  |Spaargeld of schenking bovenop eventuele overwaarde|

### Schulden & verplichtingen

Elke schuld heeft zijn eigen toetsingsmethodiek:

|Schuld             |Toetslast                                   |
|-------------------|--------------------------------------------|
|Roodstand          |2% van kredietlimiet per maand              |
|Creditcard         |2% van kaartlimiet per maand                |
|Doorlopend krediet |2% van kredietlimiet per maand              |
|Persoonlijke lening|Werkelijke maandtermijn                     |
|Studieschuld (DUO) |0,45% van *oorspronkelijke* schuld per maand|
|Private lease auto |Volledige leasetermijn per maand            |
|Partneralimentatie |Volledig bedrag per maand                   |
|Klarna / AfterPay  |Werkelijke openstaande maandtermijn         |


> Hypotheeklasten van een bestaande woning worden **niet** hier ingevoerd, maar bij “Dubbele woonlasten” in de situatiesectie.

-----

## Opslag (localStorage)

De tool slaat alle ingevulde waarden op in `localStorage` van de browser onder de sleutel `hypotheek-berekener-v1`. Dit is volledig lokaal — er worden **geen gegevens naar een server gestuurd**.

- Opslag werkt per browser + per apparaat
- De opgeslagen waarden blijven bewaard totdat je op “Alles wissen” klikt of de browserdata wist
- In privé/incognitomodus werkt de opslag alleen voor de duur van de sessie

-----

## Beperkingen & disclaimer

- Dit is een **indicatieve** berekening. De werkelijke maximale hypotheek hangt af van je volledige financiële dossier, het specifieke acceptatiebeleid van de geldverstrekker, een taxatierapport en eventuele BKR-registraties.
- De LTI-normentabel is gebaseerd op NIBUD-normen 2025. Deze normen worden jaarlijks bijgesteld.
- Raadpleeg altijd een [AFM-vergund hypotheekadviseur](https://www.afm.nl/nl-nl/professionals/registers/vergunningenregisters/wft-register).

-----

## Technische details

|Onderdeel           |Details                                                                         |
|--------------------|--------------------------------------------------------------------------------|
|Taal                |Vanilla HTML/CSS/JS — geen frameworks, geen dependencies                        |
|Externe resources   |Google Fonts (Playfair Display, DM Sans) — optioneel, valt terug op systeemfonts|
|Opslag              |`localStorage` (client-side, geen cookies, geen server)                         |
|Browserondersteuning|Alle moderne browsers (Chrome 80+, Firefox 75+, Safari 13+, Edge 80+)           |
|Bestandsgrootte     |~35 KB (single file)                                                            |

### Bestandsstructuur

```
hypotheek-berekener.html   # De volledige tool (single-file)
README.md                  # Deze documentatie
```

-----

## Licentie

Vrij te gebruiken voor persoonlijk gebruik. De berekeningslogica is een eigen clean-room implementatie gebaseerd op publiek beschikbare normentabellen (NIBUD / Staatsblad). Geen code is overgenomen van externe bronnen.
