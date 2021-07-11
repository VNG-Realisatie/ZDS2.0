API's voor Zaakgericht Werken
=====

[![Status badge][api-test-fullsuite-status]][api-test-fullsuite]
[![Build Status][docs-ci-status]][docs-ci]
![Repo Status][repo-status]

[api-test-fullsuite-status]: https://shields.api-test.nl/endpoint.svg?url=https%3A//api-test.nl/api/v1/provider-latest-badge/7419d69c-445f-48f8-a30c-31cdc72b1f80/
[api-test-fullsuite]: https://api-test.nl/server/1/c2a49a65-b749-4e6f-a006-f2ec14831714/7419d69c-445f-48f8-a30c-31cdc72b1f80/latest/
[docs-ci-status]: https://travis-ci.org/VNG-Realisatie/gemma-zaken.svg?branch=master
[docs-ci]: https://travis-ci.org/VNG-Realisatie/gemma-zaken
[repo-status]: https://img.shields.io/badge/Status-stable%2F1.0.x-brightgreen?style=plastic


**Zaakgericht werken** is een vorm van procesgericht werken waarbij de informatie die tijdens een bedrijfsproces wordt ontvangen of gecreëerd, samen met informatie over de procesuitvoering, wordt vastgelegd bij een zaak en uniform kan worden ontsloten naar alle betrokkenen.

## Doel
Deze repository bevat alles wat nodig is voor de ontwikkeling van een nieuwe standaard rond Zaakgericht Werken, welke in samenwerking tussen verschillende partijen tot stand komt. Concrete resultaten zijn meerdere OpenAPI Specificaties ten behoeve van zaakgericht werken en bijbehorende referentie-implementaties met persistente data.

## Vragen en bijdragen
Lees meer over hoe je vragen kunt stellen, bugs kunt melden en bij kunt dragen (met code of documentatie) in [`CONTRIBUTING.md`](CONTRIBUTING.md) (EN).

## Documentatie
De volgende documenten beschrijven dit project:

- We werken aan realisatie van de [Productvisie](https://vng-realisatie.github.io/gemma-zaken/productvisie/) (concept)
- Hoe u kunt [bijdragen](https://vng-realisatie.github.io/gemma-zaken/doorontwikkeling/) (inclusief het reviewproces)
- De [FAQ](docs/_content/overige/faq.md) beantwoordt vragen over het project
- De [dev-straat](https://vng-realisatie.github.io/gemma-zaken/themas/achtergronddocumentatie/ontwikkelstraat) beschrijft de development
  inrichting en tooling
- [Technische documentatie](https://vng-realisatie.github.io/gemma-zaken/ontwikkelaars/) voor developers
- [Designkeuzes en besluiten](https://vng-realisatie.github.io/gemma-zaken/themas/achtergronddocumentatie/ontwerpkeuzes) voor scrumteam, developers en stakeholders

Een hoogover overzicht van de API's voor Zaakgericht werken staat [hier](https://www.vngrealisatie.nl/producten/api-standaarden-zaakgericht-werken). De volledige documentatie zoals deze op github is beschreven is te vinden op de [github pages](https://vng-realisatie.github.io/gemma-zaken/).
De Visie en uitwerking van Zaakgericht Werken in de GEMMA Architectuur staat beschreven op het [Thema Zaakgericht werken](https://www.gemmaonline.nl/index.php/Thema_Zaakgericht_werken) op GEMMA Online.

## Beheer en ondersteuning

- Contact: standaarden.ondersteuning@vng.nl

## API spec bekijken

Zie de relevante links in dit [overzicht](https://vng-realisatie.github.io/gemma-zaken/standaard/index).

## Snelle links

**Referentie-implementaties van componenten**

* [![Build Status][zrc-ci-status]][zrc-ci]
  [Zaken API](https://github.com/vng-Realisatie/zaken-api)
* [![Build Status][drc-ci-status]][drc-ci]
  [Documenten API](https://github.com/vng-Realisatie/documenten-api)
* [![Build Status][ztc-ci-status]][ztc-ci]
  [Catalogi API](https://github.com/vng-Realisatie/catalogi-api)
* [![Build Status][brc-ci-status]][brc-ci]
  [Besluiten API](https://github.com/vng-Realisatie/besluiten-api)
* [![Build Status][nrc-ci-status]][nrc-ci]
  [Notificatiecomponent](https://github.com/VNG-Realisatie/notificaties-api)
* [![Build Status][ac-ci-status]][ac-ci]
  [Autorisaties API](https://github.com/VNG-Realisatie/autorisaties-api)

* [![Build Status][klanten-ci-status]][klanten-ci]
  [Klanten API](https://github.com/VNG-Realisatie/klanten-api)
* [![Build Status][contactmomenten-ci-status]][contactmomenten-ci]
  [Contactmomenten API](https://github.com/VNG-Realisatie/contactmomenten-api)
* [![Build Status][verzoeken-ci-status]][verzoeken-ci]
  [Verzoeken API](https://github.com/VNG-Realisatie/verzoeken-api)


**Ondersteunende tooling**

* [![Build Status][vng-api-common-ci-status]][vng-api-common]
  [Gedeelde code tussen componenten](https://github.com/VNG-Realisatie/gemma-zaken-common)
* [![Build Status][ref-lijsten-ci-status]][ref-lijsten-ci]
  [Referentielijsten API](https://github.com/VNG-Realisatie/VNG-referentielijsten)
* [ZGW Client](https://github.com/VNG-Realisatie/gemma-zds-client)
* [Demo applicatie(s)](https://github.com/VNG-Realisatie/gemma-zaken-demo)
* [Postman tests voor ZGW API's](https://github.com/VNG-Realisatie/gemma-postman-tests)

## Licentie

Copyright © VNG Realisatie 2018 - 2021

[Licensed under the EUPL](LICENCE.md)

[zrc-ci-status]: https://github.com/VNG-Realisatie/zaken-api/workflows/ci-build/badge.svg
[zrc-ci]: https://github.com/VNG-Realisatie/zaken-api/actions?query=workflow%3Aci-build
[drc-ci-status]: https://github.com/VNG-Realisatie/documenten-api/workflows/ci-build/badge.svg
[drc-ci]: https://github.com/VNG-Realisatie/documenten-api/actions?query=workflow%3Aci-build
[ztc-ci-status]: https://github.com/VNG-Realisatie/catalogi-api/workflows/ci-build/badge.svg
[ztc-ci]: https://github.com/VNG-Realisatie/catalogi-api/actions?query=workflow%3Aci-build
[brc-ci-status]: https://github.com/VNG-Realisatie/besluiten-api/workflows/ci-build/badge.svg
[brc-ci]: https://github.com/VNG-Realisatie/besluiten-api/actions?query=workflow%3Aci-build
[nrc-ci-status]: https://github.com/VNG-Realisatie/notificaties-api/workflows/ci-build/badge.svg
[nrc-ci]: https://github.com/VNG-Realisatie/notificaties-api/actions?query=workflow%3Aci-build
[ac-ci-status]: https://github.com/VNG-Realisatie/autorisaties-api/workflows/ci-build/badge.svg
[ac-ci]: https://github.com/VNG-Realisatie/autorisaties-api/actions?query=workflow%3Aci-build
[klanten-ci-status]: https://github.com/VNG-Realisatie/klanten-api/workflows/ci-build/badge.svg
[klanten-ci]: https://github.com/VNG-Realisatie/klanten-api/actions?query=workflow%3Aci-build
[contactmomenten-ci-status]: https://github.com/VNG-Realisatie/contactmomenten-api/workflows/ci-build/badge.svg
[contactmomenten-ci]: https://github.com/VNG-Realisatie/contactmomenten-api/actions?query=workflow%3Aci-build
[verzoeken-ci-status]: https://github.com/VNG-Realisatie/verzoeken-api/workflows/ci-build/badge.svg
[verzoeken-ci]: https://github.com/VNG-Realisatie/verzoeken-api/actions?query=workflow%3Aci-build


[ref-lijsten-ci-status]:  https://travis-ci.org/VNG-Realisatie/VNG-referentielijsten.svg?branch=master
[ref-lijsten-ci]:  https://travis-ci.org/VNG-Realisatie/VNG-referentielijsten

[vng-api-common-ci-status]: https://travis-ci.org/VNG-Realisatie/vng-api-common.svg?branch=master
[vng-api-common]: https://travis-ci.org/VNG-Realisatie/vng-api-common
