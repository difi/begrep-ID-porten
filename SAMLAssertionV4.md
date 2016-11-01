---
layout: default
title: SAMLAssertionV4
headtitle: ID-porten
group: ID-porten/complexType
---

Identifikator  
“http://begrep.difi.no{{ page.url | remove:".html" }}“:{{page.title}}
- Term := {{page.title}}
- Definisjon := SAML profil med støtte for både norske eID og europeiske eID autentisert via eIDAS-infrastrukturen
- Datatype :=”SAML\_2.0\_Assertion“:http://en.wikipedia.org/wiki/SAML\_2.0\#SAML\_2.0\_Assertions
- Kilde := DIFI
- Kommentar := Denne SAML-profilen er berre tilgjengeleg for tenesteeigarar som ber om det, og som utvikler støtte for innlogging av brukere med europeiske eID. Siden eIDAS-spesifikasjonene per 2015 er under utarbeidelse, kan det bli endringer i profilen i fremtiden.

h3. Attributter
h4. Attributt-kombinasjoner
Sidan profilen støttar både norske og europeiske eID, vil tilgjengelege attributter kunne variere alt etter om det er norsk eller europeisk eID som vart nytta til innlogging. For europeiske eID kan attributtane i tillegg variere mellom land. Viss attributten”AuthMethod“:\#AuthMethod har verdi Eidas, tyder dette at autentisering er føreteke med ein europeisk eID, og attributten **eIdentifier** er då unik identifikator.
Følgende 3 grunn-kombinasjoner er mulige:
table(table table-striped).
| AuthMethod | eIdentifier | uid | Beskrivelse |
| Eidas | NC/NC/xxxxxx… | <tomt> | Personen har autentisert seg med europeisk eID. Norsk D-nummer ble ikke funnet.|
| Eidas | NC/NC/xxxxxx… |”personidentifikator“:/Felles/personidentifikator | Personen har autentisert seg med europeisk eID og har norsk D-nummer. |
|”En av disse“:SAMLAssertionV1\#AuthMethod| <tomt> |”personidentifikator“:/Felles/personidentifikator | Personen har autentisert seg med norsk eID. |
For alle europeiske eID vil ID-porten forsøke å framskaffe et eventuelt norsk d-nummer/fødselsnummer fra Det Sentrale Folkeregister (DSF). Hvis et d-nummer ikke ble funnet, eller ved integrasjonsproblem mot DSF, vil ID-porten likevel fullføre autentiseringen. Dette betyr at fravær av verdi i feltet **uid** ikke entydig garanterer at personen ikke har fått tildelt d-nummer.
h4. Attributter
Denne SAML-profilen inneholder alle attributter fra”SAMLAssertionV3“:SAMLAssertionV3 :
table(table table-striped).
|*. Term |*. Beskrivelse |*. Kardinalitet |
| uid | [personidentifikator](/Felles/personidentifikator) . Norsk personnummer hvis funnet. Merk at i denne SAML-profilen kan feltet være tomt ved pålogging med europeisk eID. | 1 |
| SecurityLevel | [sikkerhetsnivaa](/Felles/sikkerhetsnivaa) | 1 |
| Culture | [språk](/Felles/spraak) | 1 |
| AuthMethod | [Autentiseringsmetode](SAMLAssertionV1#AuthMethod) | 1 |
| OnBehalfOf | Referanse til annen Offentlig Virksomhet som forespørselen er gjort på veien av | 0..1 |
| AuthnContextClassRef | Autentiseringsnivå spesifisert i henhold til kodeverk for [AuthnContextClassRef](SAMLAuthnRequest#AuthnContextClassRef) | 1 |
| [status](/Felles/status) | Kodeverk for [status](#status) | 0..1 |
| [mobiltelefonnummer](/Felles/mobiltelefonnummer) | [mobiltelefonnummer](/Felles/mobiltelefonnummer) | 0..1 |
| [epostadresse](/Felles/epostadresse) | [epostadresse](/Felles/epostadresse) | 0..1 |
| [reservasjon](/Felles/reservasjon) | [reservasjon](/Felles/reservasjon) | 0..1 |
| [postkasseleverandoerNavn](/Felles/postkasseleverandoerNavn) | [postkasseleverandoerNavn](/Felles/postkasseleverandoerNavn) | 0..1 |
I tillegg kommer eventuelle attributter fra europeisk eID-intrastruktur, eIDAS / STORK :
table.
|*.Field |*.Type |*.Values and comment |*. Kardinalitet |
|eidas-eIdentifier |String |NC/NC/xxxxxxxxxx…. |1 |
|eidas-givenName |String ||0..1 |
|eidas-surname |String |inheritedFamilyName / adoptedFamilyName |0..1 |
|eidas-inheritedFamilyName |String ||0..1 |
|eidas-adoptedFamilyName |String ||0..1 |
|eidas-gender |String |F / M |0..1 |
|eidas-nationalityCode |String |ISO 3166-1 alpha-2 |0..1 |
|eidas-maritalStatus |String |S / M / P D / W |0..1 |
|eidas-dateOfBirth |Date |YYYYMMDD / YYYYMM / YYYY |0..1 |
|eidas-countryCodeOfBirth |String |ISO 3166-3. Please note that this code is equal to ISO3166-1 alpha-2 in the majority of countries, but includes 4 letter abbreviations for disappeared countries. E.g. DDDE for the DDR or YGCS for Yugoslavia. |0..1 |
|eidas-age |Number |In years |0..1 |
|eidas-isAgeOver |Boolean |Logically this is Boolean, in technical design another domain may be chosen |0..1 |
|eidas-textResidenceAddress |Text ||0..1 |
|eidas-canonicalResidenceAddress |XML ||0..1 |
|eidas-residencePermit |String ||0..1 |
|eidas-eMail |String |RFC 822 |0..1 |
|eidas-title |Text ||0..1 |
|eidas-pseudonym |String ||0..1 |
|eidas-signedDoc |||0..1 |
|eidas-citizenQAAlevel |Number | |0..1 |
|eidas-fiscalNumber ||String |0..1 |
Vær oppmerksom på at noen land kan sende med ekstra attributter utover de som finst i eIDAS-standarden. Disse vil bli prefixet med "eidas-landskode", og så videreformidlet av ID-porten.
I tillegg utleverer vi et statusflagg for integrasjonen mot DSF:
table.
|*. Term |*. Beskrivelse |*. Kardinalitet |
|”status-dsf“:/Felles/status-dsf | Kodeverk for”status-dsf“:\#status-dsf | 0..1 |


h3. Kodeverk
h4. AuthMethod
I tillegg til”basisverdiene for norske eID“:SAMLAssertionV1\#AuthMethod kan AuthMethod ogso ha verdien:
table(table table-striped).
|*. Kodeverdi |*. Beskrivelse |
|Eidas | Autentisering utført med europeisk eID |
h4. status
”status“:/Felles/status gjelder personens status i Kontakt- og Reservasjonsregisteret, og kan ha følgende verdi:
table(table table-striped).
|*. Kodeverdi |*. Beskrivelse |
| AKTIV | Person finnes i Kontakt- og Reservasjonsregisteret |
| IKKE\_REGISTRERT | Person finnes ikke i Kontakt- og Reservasjonsregisteret, enten ikke registrert eller slettet |
| SYSTEMFEIL | ID-porten har ikke tilgang til informasjon fra Kontakt- og Reservasjonsregisteret , f.eks. ved feil i integrasjon mot registrert. |
Ved IKKE\_REGISTRERT har ikke registeret informasjon om”mobiltelefonnummer“:/Felles/mobiltelefonnummer eller”epostadresse“:/Felles/epostadresse eller”postkasseleverandoerNavn“:/Felles/postkasseleverandoerNavn , og vil ikke kunne levere ut disse elementene til Offentlig virksomhet.
Ved autentisering med europeisk eID, er det frivillig for personer som har fått tildelt norsk D-nummer/fødselsnummer å oppgi kontaktopplysninger til Kontakt- og Reservasjonsregisteret. Personer som ikke har fått tildet norsk D-nummer/fødselsnummer, har ikke mulighet til å oppgi kontaktopplysninger.
For utenlandske innbyggere, blir Kontakt- og reservasjonsregisteret kun sjekket dersom det er oppnådd en entydig kobling mot norsk D-nummer/fødselsnummer. Dette kan skje ved manglende kobling eller ved feilsituasjoner mot DSF. Informasjon fra Kontakt-og reservasjonsregisteret vil da mangle.


h4. status-dsf
”status-dsf“:/Felles/status-dsf gjelder ID-portens integrasjonsstatus mot Det Sentrale Folkeregisteret (DSF).
table(table table-striped).
|*. Kodeverdi |*. Beskrivelse |
| OK | ID-porten har som del av innlogging gjennomført en spørring mot DSF uten tekniske feil|
| SYSTEMFEIL | ID-porten har ikke tilgang til informasjon fra Det Sentrale Folkeregisteret , f.eks. ved feil i integrasjon mot registrert. |
| FLERETREFF | Oppslag mot DSF har resultert i flere mulige treff, og ID-porten kan ikke gjøre en garantert kobling mellom utenlandsk eID og D-nummer i DSF |
| IKKESJEKKET| ID-porten mangler tilstrekkelig informasjon til å kunne gjøre en spørring mot DSF, for eksempel hvis navn eller fødselsdato mangler på utenlandsk bruker |


h4. Eksempel

Eksempel på europeisk eID utan D-nummer:
\<pre class=”brush: xml; toolbar: false“\>
 <saml:AttributeStatement>
 <saml:Attribute Name="uid">
 <saml:AttributeValue xmlns:xs="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:type="xs:string"></saml:AttributeValue>
 </saml:Attribute>
 <saml:Attribute Name="Culture">
 <saml:AttributeValue xmlns:xs="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:type="xs:string">en</saml:AttributeValue>
 </saml:Attribute>
 <saml:Attribute Name="AuthMethod">
 <saml:AttributeValue xmlns:xs="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:type="xs:string">Eidas</saml:AttributeValue>
 </saml:Attribute>
 <saml:Attribute Name="SecurityLevel">
 <saml:AttributeValue xmlns:xs="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:type="xs:string">3</saml:AttributeValue>
 </saml:Attribute>
 <saml:Attribute Name="eidas-eIdentifier">
 <saml:AttributeValue xmlns:xs="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:type="xs:string">SE/NO/74629XY34+D/S</saml:AttributeValue>
 </saml:Attribute>
 <saml:Attribute Name="eidas-givenName">
 <saml:AttributeValue xmlns:xs="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:type="xs:string">Nomen</saml:AttributeValue>
 </saml:Attribute>
 <saml:Attribute Name="eidas-surname">
 <saml:AttributeValue xmlns:xs="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:type="xs:string">Nescio</saml:AttributeValue>
 </saml:Attribute>
 <saml:Attribute Name="eidas-dateOfBirth">
 <saml:AttributeValue xmlns:xs="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:type="xs:string">19650821</saml:AttributeValue>
 </saml:Attribute>
 </saml:AttributeStatement>
\</pre\>
Eksempel på innlogging med norsk eID:
\<pre class=”brush: xml; toolbar: false“\>
 <saml:AttributeStatement>
 <saml:Attribute Name="uid">
 <saml:AttributeValue xmlns:xs="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:type="xs:string">03015561903</saml:AttributeValue>
 </saml:Attribute>
 <saml:Attribute Name="Culture">
 <saml:AttributeValue xmlns:xs="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:type="xs:string">nb</saml:AttributeValue>
 </saml:Attribute>
 <saml:Attribute Name="epostadresse">
 <saml:AttributeValue xmlns:xs="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:type="xs:string">03015561903-test@minid.norge.no</saml:AttributeValue>
 </saml:Attribute>
 <saml:Attribute Name="mobiltelefonnummer">
 <saml:AttributeValue xmlns:xs="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:type="xs:string">03015561903</saml:AttributeValue>
 </saml:Attribute>
 <saml:Attribute Name="status">
 <saml:AttributeValue xmlns:xs="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:type="xs:string">AKTIV</saml:AttributeValue>
 </saml:Attribute>
 <saml:Attribute Name="reservasjon">
 <saml:AttributeValue xmlns:xs="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:type="xs:string">NEI</saml:AttributeValue>
 </saml:Attribute>
 <saml:Attribute Name="AuthMethod">
 <saml:AttributeValue xmlns:xs="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:type="xs:string">Minid-PIN</saml:AttributeValue>
 </saml:Attribute>
 <saml:Attribute Name="SecurityLevel">
 <saml:AttributeValue xmlns:xs="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:type="xs:string">3</saml:AttributeValue>
 </saml:Attribute>
 <saml:Attribute Name="postkasseleverandoerNavn">
 <saml:AttributeValue xmlns:xs="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:type="xs:string">Digipost test operator</saml:AttributeValue>
 </saml:Attribute>
 <saml:Attribute Name="eidas-eIdentifier">
 <saml:AttributeValue xmlns:xs="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:type="xs:string"></saml:AttributeValue>
 </saml:Attribute>
 </saml:AttributeStatement>

\</pre\>
Eksempel på europeisk eID med D-nummer og der personen har oppgitt kontaktopplysninger til Kontakt- og Reservasjonsregistert:
\<pre class=”brush: xml; toolbar: false"\>

<saml:AttributeStatement>
 <saml:Attribute Name="uid">
 <saml:AttributeValue xmlns:xs="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:type="xs:string">45678901234</saml:AttributeValue>
 </saml:Attribute>
 <saml:Attribute Name="Culture">
 <saml:AttributeValue xmlns:xs="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:type="xs:string">en</saml:AttributeValue>
 </saml:Attribute>
 <saml:Attribute Name="AuthMethod">
 <saml:AttributeValue xmlns:xs="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:type="xs:string">Eidas</saml:AttributeValue>
 </saml:Attribute>
 <saml:Attribute Name="SecurityLevel">
 <saml:AttributeValue xmlns:xs="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:type="xs:string">3</saml:AttributeValue>
 </saml:Attribute>

<saml:Attribute Name="epostadresse">
 <saml:AttributeValue xmlns:xs="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:type="xs:string">03015561903-test@minid.norge.no</saml:AttributeValue>
 </saml:Attribute>
 <saml:Attribute Name="mobiltelefonnummer">
 <saml:AttributeValue xmlns:xs="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:type="xs:string">+461234567890</saml:AttributeValue>
 </saml:Attribute>
 <saml:Attribute Name="status">
 <saml:AttributeValue xmlns:xs="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:type="xs:string">AKTIV</saml:AttributeValue>
 </saml:Attribute>
 <saml:Attribute Name="reservasjon">
 <saml:AttributeValue xmlns:xs="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:type="xs:string">NEI</saml:AttributeValue>
 </saml:Attribute>

<saml:Attribute Name="eidas-eIdentifier">
 <saml:AttributeValue xmlns:xs="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:type="xs:string">SE/NO/74629XY34+D/S</saml:AttributeValue>
 </saml:Attribute>
 <saml:Attribute Name="eidas-givenName">
 <saml:AttributeValue xmlns:xs="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:type="xs:string">Nomen</saml:AttributeValue>
 </saml:Attribute>
 <saml:Attribute Name="eidas-surname">
 <saml:AttributeValue xmlns:xs="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:type="xs:string">Nescio</saml:AttributeValue>
 </saml:Attribute>
 <saml:Attribute Name="eidas-dateOfBirth">
 <saml:AttributeValue xmlns:xs="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:type="xs:string">19650821</saml:AttributeValue>
 </saml:Attribute>

<saml:Attribute Name="eidas-eMail">
 <saml:AttributeValue xmlns:xs="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:type="xs:string">denneKanVereUlikKRR@ein.anna.domene</saml:AttributeValue>
 </saml:Attribute>

</saml:AttributeStatement>

</pre>
</pre>
