---
title: ID-porten
pageid: pilot-introduction
layout: default
description: SAML
isHome: true
---


ID-porten er et nav/tillitsanker for offentlig virksomheter. ID-porten knytter de offentlige virksomhetene og e-ID leverandørene sammen.

## Integrasjonsguide:

Integrasjonsguide er tilgjengelig på [DIFI sin samarbeidsportal](http://samarbeid.difi.no)

## Autentiseringsforespørsel

[SAML AuthnRequest](2_authnrequest)

## SAML2Assertion profiler

Responsen fra ID-porten vil være en av følgende forskjellige profiler:

|Profilnavn|Beskrivelse|
|----------|-----------|
|[SAMLAssertionV1](http://begrep.difi.no/ID-porten/)|Standard profil|
|[SAMLAssertionV2](http://begrep.difi.no/ID-porten/)|FORELDET, kun tilgjengelig for å være bakoverkompatibel|
|[SAMLAssertionV3](http://begrep.difi.no/ID-porten/)|Utvidet profil med informasjon fra kontakt og reservasjonsregisteret|
|[SAMLAssertionV5](3_SAMLAssertionv5)|Utvidet profil som i tillegg til norske eID støtter autentisering av  europeiske eID gjennom eIDAS-infrastrukturen, samt kan utvides med flere utenlandske eID senere|

