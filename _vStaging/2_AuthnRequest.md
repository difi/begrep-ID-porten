---
title: SAML AuthnRequest
pageid: authnrequest
layout: default
description: Dokumentasjon av akseptert AuthnRequest mot ID-porten
isHome: false
---

Den informasjon som overføres til ID-porten for å forespørre en autentisering.

I ID-Porten SAML2 profilen MÅ forespørselen signeres. Signaturen plasseres i Signatur forespørsel strengen beskrevet for denne bindingen, og ikke i selve XML meldingen. Slik:

```
SAMLRequest=<req>&SigAlg=<alg>&Signature=<SIGNATUR>
```

## Attributer


| Term | Beskrivelse | Kardinalitet |
| --- | --- | --- |
| AuthnContextClassRef | Autentiseringsnivå spesifisert i henhold til kodeverk for [AuthnContextClassRef](#AuthnContextClassRef) beskrevet under | 0..1 |
| ForceAuth | Vil kreve at brukeren gjennomfører autentisering . | 0..1 |
| locale | [spraak](/Felles/spraak), se under for hvilke språk som er støttet | 0..1 |
| OnBehalfOf | Referanse til annen Offentlig Virksomhet som forespørselen er gjort på veien av | 0..1 |

## Kodeverk

### AuthnContextClassRef

Kodeverk for AuthnContextClassRef er definert som under, der hver AuthnContextClassRef er knyttet til et spesielt 
[sikkerhetsnivaa](/Felles/sikkerhetsnivaa) slik:

| AuthnContextClassRef | [sikkerhetsnivaa](/Felles/sikkerhetsnivaa) |
| --- | --- | --- |
| urn:oasis:names:tc:SAML:2.0:ac:classes:Unspecified | 3 |
| urn:oasis:names:tc:SAML:2.0:ac:classes:PasswordProtectedTransport | 3 |
| urn:oasis:names:tc:SAML:2.0:ac:classes:SmartcardPKI | 4 |

ID-porten vil tolke alle forespørsler til AuthnContextClassRef er urn:oasis:names:tc:SAML:2.0:ac:classes:Unspecified om RequestedAuthnContext ikke er inkludert i \<AuthnRequest\>.

### Språk

Følgende språk er støttet i forespørselen:
| ISO 639-1 kode | Språk |
| --- | --- |
| nb | Bokmål |
| nn | nynorsk |
| se | Samisk |
| en | Engelsk |

## eksempel

Eksempel forespørsel:

```
<samlp:RequestedAuthnContext xmlns:samlp="urn:oasis:names:tc:SAML:2.0:protocol" Comparison="minimum">
 <saml:AuthnContextClassRef xmlns:saml="urn:oasis:names:tc:SAML:2.0:assertion">
 urn:oasis:names:tc:SAML:2.0:ac:classes:PasswordProtectedTransport
 </saml:AuthnContextClassRef>
</samlp:RequestedAuthnContext>
```

Eksempel på bruk av OnBehalfOf:

```
<samlp:AuthnRequest xmlns:samlp="urn:oasis:names:tc:SAML:2.0:protocol" ...>
 <saml:Issuer xmlns:saml="urn:oasis:names:tc:SAML:2.0:assertion">TJENESTELEVERANDOR</saml:Issuer>
 …
 <samlp:Extensions xmlns:samlp="urn:oasis:names:tc:SAML:2.0:protocol">
 <idpe:OnBehalfOf xmlns:idpe="https://idporten.difi.no/idporten-extensions">TJENESTEEIER</idpe:OnBehalfOf>
 </samlp:Extensions>
 …
</samlp:AuthnRequest>
```
