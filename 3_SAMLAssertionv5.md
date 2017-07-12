---
title: ID-porten SAML assertion profile v5
pageid: SAMLAssertionv5
layout: default
description: ID-porten profil som støtter innlogging med utenlandsk eID gjennom eIDAS-infrastrukuren
isHome: false
resource: true
category: vStaging
---

## Introduksjon

SAML-profil som støtter innlogging med utenlandsk eID gjennom eIDAS-infrastrukuren. Denne SAML-profilen er berre tilgjengeleg for tenesteeigarar som ber om det. For meir info om eIDAS, sjå [https://ec.europa.eu/cefdigital/wiki/display/CEFDIGITAL/How+does+it+work+-+eIDAS+solution](https://ec.europa.eu/cefdigital/wiki/display/CEFDIGITAL/How+does+it+work+-+eIDAS+solution).

ID-porten er basert på SAML2 Web Browswer SSO profile.


## Identifisering

Sidan profilen støttar både norske og europeiske eID, vil tilgjengelege attributter kunne variere alt etter om det er norsk eller europeisk eID som vart nytta til innlogging. Viss attributten [AuthMethod](#authmethod) har verdi Eidas, tyder dette at autentisering er føreteke med ein europeisk eID, og attributten *PersonIdentifier* er då unik identifikator.

| AuthMethod | PersonIdentifier | uid | Beskrivelse |
| --- | ---- | --- | --- |
| Eidas | CC/NO/xxxxxx… | <tomt> | Personen har autentisert seg med europeisk eID. Norsk D-nummer ble ikke funnet.|
| Eidas | CC/NO/xxxxxx… | norsk personidentifikator | Personen har autentisert seg med europeisk eID og har norsk D-nummer. |
| [En av disse](https://begrep.difi.no/ID-porten/SAMLAssertionV1)| <tomt> | norsk personidentifikator | Personen har autentisert seg med norsk eID. |

For alle europeiske eID vil ID-porten forsøke å framskaffe et eventuelt norsk d-nummer/fødselsnummer fra Det Sentrale Folkeregister (DSF). Hvis et d-nummer ikke ble funnet, eller ved integrasjonsproblem mot DSF, vil ID-porten likevel fullføre autentiseringen, dersom ikke tjenesten er manuelt konfigurert til kreve norsk personidentifikator. Dette betyr at fravær av verdi i feltet *uid* ikke entydig garanterer at personen ikke har fått tildelt d-nummer

Kvaliteten på koblinga fremgår av attributten [IdentityMatch](#identitymatch)


## Attributter


Denne SAML-profilen inneholder alle attributter fra [SAMLAssertionV3](https://begrep.difi.no/ID-porten/SAMLAssertionV3) :

| *Term* | *Beskrivelse* | *Kardinalitet* |
| --- | --- | --- |
| uid | [personidentifikator](https://begrep.difi.no/Felles/personidentifikator) . Norsk personnummer hvis funnet. Merk at i denne SAML-profilen kan feltet være tomt ved pålogging med europeisk eID. | 0..1 |
| SecurityLevel | [sikkerhetsnivaa](https://begrep.difi.no/Felles/sikkerhetsnivaa) | 1 |
| Culture | [språk](https://begrep.difi.no/Felles/spraak) | 1 |
| AuthMethod | [Autentiseringsmetode](#AuthMethod) | 1 |
| [reservasjon](https://begrep.difi.no/Felles/reservasjon) | [reservasjon](https://begrep.difi.no/Felles/reservasjon) | 0..1 |
| [epostadresse](https://begrep.difi.no/Felles/epostadresse) | [epostadresse](https://begrep.difi.no/Felles/epostadresse) | 0..1 |
| [mobiltelefonnummer](https://begrep.difi.no/Felles/mobiltelefonnummer) | [mobiltelefonnummer](https://begrep.difi.no/Felles/mobiltelefonnummer) | 0..1 |
| [postkasseleverandoerNavn](https://begrep.difi.no/Felles/postkasseleverandoerNavn) | [postkasseleverandoerNavn](https://begrep.difi.no/Felles/postkasseleverandoerNavn) | 0..1 |
| [status](https://begrep.difi.no/Felles/status) | Kodeverk for [status](#status) | 0..1 |
| IdentityMatch | Kvalitetsindikator for kobling ('matching') mot norsk personidentifikator | 0..1 |
| eidas-PersonIdentifier  |String |CC/NO/xxxxxxxxxx… &nbsp;  CC er ISO3166-1 landkode som har utstedt den aktuelle eIDen. | 0..1 | 
| eidas-CurrentFamilyName |String | Etternavn | 0..1 |
| eidas-CurrentGivenName  |String | Fornavn | 0..1 |
| eidas-DateOfBirth       |Date   | YYYY-MM-DD | 0..1 |
| eidas-samlResponse       |String | Den komplette, dekrypterte SamlRespons-meldingen som ID-porten mottok fra eIDAS.  Sektor-spesifikke og valgfrie attributter vil finnes her|
| OnBehalfOf | Referanse til annen Offentlig Virksomhet som forespørselen er gjort på vegne av | 0..1 |


I fremtiden kan profilen bli utvidet med flere attributter, dersom nye eID blir koblet på løsningen.


## Kodeverk

Denne SAML-profile utvider kodeverket for flere av de eksisterende attributtene i ID-porten.

### sikkerhetsnivaa

se [http://begrep.difi.nohttps://begrep.difi.no/Felles/sikkerhetsnivaa](http://begrep.difi.nohttps://begrep.difi.no/Felles/sikkerhetsnivaa) for eksisternde verdier.

| sikkerhetsnivaa | forklaring |
| --- | --- |
| 3 | Norsk sikkerhetsnivå 3 |
| 4 | Norsk sikkerhetstnivå 4 |
| substantial | eIDAS mellomhøyt nivå |
| high        | eIDAS høyt nivå|


### AuthMethod

Se [http://begrep.difi.no/ID-porten/SAMLAssertionV1#AuthMethod](http://begrep.difi.no/ID-porten/SAMLAssertionV1#AuthMethod) for eksistende verdier.

I tillegg innfører vi per 1.1.2017 to nye verdier (kan blir utvidet med flere senere)

| AuthMethod | forklaring |
| --- | --- |
| Eidas | Bruker har logget seg på med en eID som er formelt notifisert under eIDAS reguleringen.  |
| Eidas-nonnotified | Bruker har logget seg på gjennom eIDAS med en eID som ikke er formelt notifisert, men der Norge og avgivende land har en bilateral avtale for anerkjenning |


### IdentityMatch

Kvalitetsindikator for kobling ('matching') mot norsk personidentifikator

| IdentityMatch | forklaring |
| --- | --- |
| UNAMBIGUOS | Identifikator fra utenlandsk eID'en har en entydig kobling mot identitet i Det Sentrale Folkeregister |
| BEST_EFFORT | Attributter fra utenlandsk eID er benyttet til koble mot sannsynlig identitet i Det Sentrale Folkeregister.  (For eksempel: navn og fødselsdato stemmer med en person i DSF) |
| CACHED | Kobling mot norsk personidentifikator er basert på lagret informasjon i ID-porten, og ikke som del av denne innloggingen.  (dette kan typisk skje ved midlertidige integrasjonsfeil mellom ID-porten og DSF)|
| ERROR | Det oppstod en feil ved forsøket på å koble utenlandsk eID mot norsk personidentifikator (Dette kan skje feks ved feil i kommuniksajonen mellom ID-porten og Det Sentrale Folkeregisteret|
|NOT_FOUND | Ingen treff ved forsøk på kobling av utenlandsk eID mot norsk personidentifikator i Det Sentrale Folkeregister)|
|SELF_DECLARED | Norsk personidentifikator er basert på opplysninger som brukeren selv har oppgitt (Brukeren har for eksempel koblet sin Facebook-konto med ID-porten|
