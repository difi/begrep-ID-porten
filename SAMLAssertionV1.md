---
layout: default
title: SAMLAssertionV1
headtitle: ID-porten
group: ID-porten/complexType
---

Identifikator  
“http://begrep.difi.no{{ page.url | remove:".html" }}“:{{page.title}}
- Term := {{page.title}}
- Definisjon := Informasjon om en Person utlevert via ID-porten, standard profil.
- Datatype :=”SAML\_2.0\_Assertion“:http://en.wikipedia.org/wiki/SAML\_2.0\#SAML\_2.0\_Assertions
- Kilde := DIFI
- Kommentar := Den informasjon som utleveres i ID-porten sin standard SAML2 profil ved Autentisering
h4. Attributer
table(table table-striped).
|*. Term |*. Beskrivelse |*. Kardinalitet |
| uid | [personidentifikator](/Felles/personidentifikator) | 1 |
| SecurityLevel | [sikkerhetsnivaa](/Felles/sikkerhetsnivaa) | 1 |
| Culture | [språk](/Felles/spraak) | 1 |
| AuthMethod | [Autentiseringsmetode](#AuthMethod) | 1 |
| OnBehalfOf | Referanse til annen Offentlig Virksomhet som forespørselen er gjort på veien av | 0..1 |
| AuthnContextClassRef| Autentiseringsnivå spesifisert i henhold til kodeverk for [AuthnContextClassRef](SAMLAuthnRequest#AuthnContextClassRef) | 1 |
h4. Kodeverk
h5. AuthMethod
table.
|*. AuthMetod |\_. Beskrivelse |
| Minid-PIN | Bruker har logget seg på med PIN koder fra PIN kode ark. |
| Minid-OTC | Bruker har logget seg på med engangskode sendt på SMS |
| Buypass | Bruker har logget seg på med smartkort fra Buypass |
| Commfides | Bruker har logget seg på med USB-pen med e-ID fra Commfides |
| BankID | Bruker har logget seg på med BankID med kodebrikke |
| BankID Mobil | Bruker har logget seg på med BankID på mobil |

h4. Eksempel
\<pre class=”brush: xml; toolbar: false"\>

<saml:AttributeStatement>
 <saml:Attribute Name="uid">
 <saml:AttributeValue xmlns:xs="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:type="xs:string">03015561903</saml:AttributeValue>
 </saml:Attribute>
 <saml:Attribute Name="Culture">
 <saml:AttributeValue xmlns:xs="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:type="xs:string">nb</saml:AttributeValue>
 </saml:Attribute>
 <saml:Attribute Name="AuthMethod">
 <saml:AttributeValue xmlns:xs="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:type="xs:string">Minid-PIN</saml:AttributeValue>
 </saml:Attribute>
 <saml:Attribute Name="SecurityLevel">
 <saml:AttributeValue xmlns:xs="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:type="xs:string">3</saml:AttributeValue>
 </saml:Attribute>
 </saml:AttributeStatement>

</pre>
