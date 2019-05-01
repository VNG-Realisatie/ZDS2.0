---
title: "Audit trail"
date: '01-05-2019'
weight: 50
---

Gebaseerd op: User Story [#722](https://github.com/VNG-Realisatie/gemma-zaken/issues/722)

## Inleiding

Consumers willen op een eenvoudige manier een audit trail kunnen opvragen zoals
die nu veelal wordt weergeven in monolithische zaaksystemen.

We hanteren voor het opstellen van een audit trail, de volgende definitie:

> De audit trail bevat voldoende gegevens om achteraf te kunnen herleiden (1) 
> welke essentiële handelingen (2) wanneer door (3a) wie of (3b) vanuit welk 
> systeem (4) met welk resultaat zijn uitgevoerd.
> Tot essentiële handelingen worden in ieder geval gerekend: opvoeren en 
> afvoeren posten, statusveranderingen met wettelijke, financiële of voor de 
> voortgang van het proces, de zaak of de klant beslissende gevolgen.

Bron: [NORA](https://www.noraonline.nl/wiki/Inhoud_audit_trail)

We laten de relatie met logging (in het algemeen) en doelbinding volgens de AVG
buiten beschouwing. Hier zijn andere oplossingen voor in de maak, zoals 
[NLx](https://nlx.io).

## API implementatie

### Endpoint

De API wordt gerealiseerd als alleen-lezen endpoint binnen de API van het 
component, waarbij de resource "audittrail" wordt ontsloten op het gelijknamige
endpoint. Voor het ZRC zal dit dus zijn: `/api/v1/audittrail`.

De autit trail resource *kan* ingeladen worden in de OAS van het component 
middels een referentie maar mag ook inline worden opgenomen in de OAS van het 
component zelf.

**Rationale**

De audit trail API...

1. ...wordt beschikbaar in een zelfstandig component worden waar alle andere 
   componenten hun audit regels naar toe sturen.
2. ...wordt onderdeel van de component API.

We realiseren geen apart component voor de audit trail waar alle componenten
hun logging heen sturen. Dit zou een synchrone afhankelijkheid creëeren en er
gaat potentieel veel informatie over het netwerk wat veel overhead veroorzaakt,
zelfs als niemand deze audit trail ooit raad pleegt. Ten slotte staat deze 
opzet een eventueel centraal logging component niet in de weg.

De audit trail API wordt dus onderdeel van elk component. Er zijn 2 keuzes, de 
audit trail API...

1. ...krijgt een zelfstandige API naast de component API 
   (`example.com/zrc/api/v1` en `example.com/zrc/audittrail/api/v1`).
2. ...wordt onderdeel van de component API 
   (`example.com/zrc/api/v1/audittrail`).

Bij het NRC is voor het ontvangen van notificaties door componenten gekozen 
voor een zelfstandige API. Dit voorkomt dat een wijziging voor de audit trail 
API alle API's van componenten raakt. Echter, bij het NRC geeft de consumer 
zelf aan waar deze API te vinden is. Bij de audit trail is hiervan geen sprake
en dus moet de API consistent en snel te vinden zijn, en het is in essentie ook
echt een onderdeel van het component.

### Attributen

`uuid` (automatisch)

Unieke identificatie van de audit regel.

`bron` (automatisch)

De naam van get component waar de wijziging in is gedaan. Hoewel dit attribuut 
in de context van de API niet relevant lijkt, aangezien de API onderdeel is van 
het component. Mocht deze API echter gebruikt worden in een geaggregeerde 
context, dan blijft het formaat voor consumers gelijk.

`applicatieId` (verplicht)

Unieke identificatie van de applicatie, binnen de organisatie. Deze komt 
overeen met het `client_id` attribuut uit de JWT.

`applicatieWeergave` (optioneel)

Vriendelijke naam van de applicatie. Deze kan worden afgeleid uit het `label` 
attribuut van de `Applicatie` resource in het Atorisatie Component (AC).

`gebruikersId` (verplicht) 

Unieke identificatie van de gebruiker, binnen de organisatie. Deze moet uit de 
JWT worden gehaald.

*TODO: Moet nog worden toegevoegd aan het JWT en relevante documentatie*

`gebruikersWeergave` (optioneel)

Vriendelijke naam van de gebruiker. Deze moet uit de JWT worden gehaald.

*TODO: Moet nog worden toegevoegd aan het JWT en relevante documentatie*

`actie` (verplicht)

De uitgevoerde handeling *zoals bij notificaties*.

`actieWeergave` (optioneel)

Vriendelijke naam van de actie. Bijvoorbeeld als een relatie tussen 
een document en een zaak wordt aangemaakt: "gekoppeld aan Zaak MOR-000001".

*TODO: Wellicht ook toevoegen aan het NRC (buiten scope)*

`resultaat` (verplicht)

HTTP status code van de API response van de uitgevoerde handeling. Een HTTP
status code van "200" of "201" is bijvoorbeeld een succesvol uitgevoerde 
handeling, terwijl een "403" aangeeft dat de gebruiker of applicatie het wel
geprobeerd heeft maar de handeling is niet uitgevoerd.

`hoofdObject` (verplicht)

De URL naar het hoofd object van een component *zoals bij notificaties*. Bij 
het ZRC is dit dus altijd de URL naar een zaak.

`resource` (verplicht)

De resource naam *zoals bij notificaties*.

`resourceUrl` (verplicht)

De URL naar het object *zoals bij notificaties*.

`resourceWeergave` (optioneel)

Vriendelijke identificatie van het object. Bijvoorbeeld de zaak identificatie 
of de omschrijving van een status.

`toelichting` (optioneel)

Toelichting waarom de handeling is uitgevoerd. Dit kan handig zijn voor sommige
handelingen waarbij additionele context gewenst is, zoals het ophogen van een
archiveringstermijn of een correctie buiten het reguliere proces om.

`aanmaakdatum` (automatisch)

De datum waarom de handeling is gedaan.

#### TODO: Extra attributen

In overweging om op te nemen:

* `verschillen` -- Een lijst met de wijzigingen.
* `weergave` -- De audit trail regel op vriendelijke wijze samengesteld.

#### Voorbeeld

```http
GET /api/v1/zrc/audittrail/
[
  {
    "uuid": "311cf2",
    "bron": "ZRC",
    "applicatieId": "demo-app",
    "applicatieWeergave": "Demo applicatie",
    "gebruikersId": "14",
    "gebruikersWeergave": "Joeri Bekker",
    "actie": "create",
    "actieWeergave": "",
    "resultaat": 201,
    "hoofdObject": "https://www.example.com/api/v1/zaken/5ab6e2",
    "resource": "status",
    "resourceUrl": "https://www.example.com/api/v1/statussen/11cb71",
    "resourceWeergave": "Ingediend",
    "toelichting": "",
    "aanmaakdatum": "2019-05-05T11:53:18.090384Z",
  }
]
```

Hiermee kan de volgende (eenvoudige) audit regel worden opgesteld:

```
<aanmaakdatum> <resource> "<resourceWeergave>" is <resultaat> <actie/actieWeergave> in <bron> door <gebruikersWeergave> (<gebruikersId>) via <applicatieWeergave> (<applicatieId)
```

Dat als instantie vertaald kan worden naar:

```
5 mei 2019 11:53 Status "Ingediend" is succesvol aangemaakt in ZRC door Joeri Bekker (14) via Demo Applicatie (demo-app).
```

### Query parameters

Er kan worden gefilterd op:

* `applicatieId` (`exact` en `in`)
* `gebruikersId` (`exact` en `in`)
* `actie` (`exact` en `in`)
* `resultaat` (`exact`, `in`, `lte` en `gte`)
* `hoofdObject`
* `resource` (`exact` en `in`)
* `resourceUrl`
* `aanmaakdatum` (`exact`, `lte` en `gte`)

En gesorteerd worden op:

* `aanmaakdatum` (`asc` en `desc`)

#### Voorbeelden

Zo kan bijvoorbeeld een audit trail worden opgevraagd van een bepaalde zaak:

```http
GET /api/v1/zrc/audittrail?
  hoofdObject = https://www.example.com/api/v1/zaken/5ab6e2
```

Of, om alle foutmeldingen in een bepaalde periode, door een bepaald persoon 
weer te geven:

```http
GET /api/v1/zrc/audittrail?
  resultaat__gte = 300 &
  gebruikersId = 14 &
  aanmaakdatum__gte = 2019-01-01 &
  aanmaakdatum__lte = 2019-01-31
```

### Samenstellen van volledige audit trail

Tot nu toe hebben we alleen een audit trail besproken van een enkel component.
Als er echter bij een zaak ook documenten en besluiten worden gemaakt in andere
componenten, dan zou deze idealiter in een volledige audit trail van de zaak
terug komen. Afhankelijk van de gebruikersinterface kan dit wel of niet nodig
zijn.

Alle componenten gaan de audit trail endpoint ontsluiten. Als de zaak wordt
opgevraagd, dan worden ook de gerelateerde documenten en besluiten bekend zoals
die leven in respectievelijk het DRC en het BRC. Hiervoor zal dus 1 call per
component nodig zijn om de volledige audit trail te verkrijgen.

Overigens wordt dit niet persé eenvoudiger als alles in 1 audit trail component
zou zitten. Immers moeten nog steeds alle URLs van de hoofdObjecten bekend zijn 
en worden opgevraagd.