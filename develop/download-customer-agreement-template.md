---
title: Pobierz link pobierania dla Umowa z Klientem Microsoft szablonu
description: Pobierz link pobierania dla Umowa z Klientem Microsoft szablonu.
ms.date: 02/12/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: cychua
ms.author: cychua
ms.openlocfilehash: fccb9e3d4a837f3e8043f8c7ae1e3911d819afd7
ms.sourcegitcommit: d20e7d572fee09a83a4b23a92da7ff09cfebe75a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/10/2021
ms.locfileid: "111906525"
---
# <a name="get-a-download-link-for-the-microsoft-customer-agreement-template"></a>Pobierz link pobierania dla Umowa z Klientem Microsoft szablonu

**Dotyczy:** Partner Center

**Nie dotyczy:** Partner Center obsługiwane przez firmę 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government

Zasób **AgreementDocument** jest obecnie obsługiwany Partner Center tylko w chmurze publicznej firmy Microsoft.

W tym artykule opisano, jak uzyskać link do Umowa z Klientem Microsoft szablonu na podstawie kraju i języka klienta.

## <a name="prerequisites"></a>Wymagania wstępne

- Jeśli używasz zestawu SDK platformy Partner Center .NET, wymagana jest wersja 1.14 lub nowsza.

- Poświadczenia zgodnie z opisem w te [Partner Center uwierzytelniania.](./partner-center-authentication.md) Ten scenariusz obsługuje tylko uwierzytelnianie app+user.

- Kraj klienta, do którego ma Umowa z Klientem Microsoft szablon klienta.

- Język, w którym Umowa z Klientem Microsoft szablon powinien być zlokalizowany.

> [!IMPORTANT]
>
> - Ta Umowa z Klientem Microsoft jest specyficzna dla kraju. Podczas żądania linku do pobrania Umowa z Klientem Microsoft należy określić właściwy kraj na podstawie lokalizacji klienta. lub listę obsługiwanych krajów, zapoznaj się [z listą obsługiwanych krajów i języków.](#list-of-supported-countries-and-languages)
>
> - W niektórych krajach Umowa z Klientem Microsoft w wielu językach. Aby uzyskać najlepszą obsługę klienta, wybierz język, który najlepiej odpowiada potrzebom klienta. Aby uzyskać listę obsługiwanych języków, zapoznaj się [z listą obsługiwanych krajów i języków.](#list-of-supported-countries-and-languages)
> - Ta metoda jest obsługiwana tylko w przypadku Umowa z Klientem Microsoft.

## <a name="net"></a>.NET

Aby pobrać link do pobrania Umowa z Klientem Microsoft szablonu:

1. Pobierz metadane umowy dla Umowa z Klientem Microsoft. Należy uzyskać **templateId** Umowa z Klientem Microsoft. Aby uzyskać więcej informacji, zobacz [Get agreement metadata for Umowa z Klientem Microsoft](get-customer-agreement-metadata.md)(Uzyskiwanie metadanych umowy dla Umowa z Klientem Microsoft ).

   ```csharp
   // IAggregatePartner partnerOperations;

   string agreementType = "MicrosoftCustomerAgreement";

   AgreementMetaData microsoftCustomerAgreementDetails = partnerOperations.AgreementDetails.   ByAgreementType(agreementType).Get().Items.Single();
   ```

2. Użyj kolekcji IAggregatePartner.AgreementTemplates.

3. Wywołaj **metodę ById** i określ **wartość templateId** Umowa z Klientem Microsoft.

4. Pobierz właściwość **Document.**

5. Wywołaj **metodę ByCountry** i określ kraj klienta, do którego ma zastosowanie szablon umowy. Jeśli metoda nie zostanie *określona,* zapytanie będzie domyślnie oznaczać wartość USA. Aby uzyskać listę obsługiwanych kodów krajów, zapoznaj się [z listą obsługiwanych krajów i języków.](#list-of-supported-countries-and-languages) W tej metodzie jest **zróżnicowa wielkość liter.**

6. Wywołaj **metodę ByLanguage** i określ język, w jakim szablon umowy powinien być zlokalizowany. Zapytanie domyślnie określa wartość *en-US,* jeśli metoda nie została określona lub podany kod kraju nie jest obsługiwany dla określonego kraju. Aby uzyskać listę obsługiwanych kodów języków, zapoznaj [się z listą obsługiwanych krajów i języków.](#list-of-supported-countries-and-languages)

7. Wywołaj **metodę Get** lub **GetAsync.**

   ```csharp
   // IAggregatePartner partnerOperations;

   string customerCountry = "US";

   string languageForLocalization = "en-US";

   var agreementDocument = partnerOperations.   AgreementTemplates.ById   (microsoftCustomerAgreementDetails.   TemplateId).Document.ByCountry   (customerCountry).ByLanguage   (languageForLocalization).Get();
   ```

Kompletny przykład można znaleźć w klasie [GetAgreementDetails](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples/blob/master/Source/Partner%20Center%20SDK%20Samples/Agreements/GetAgreementDetails.cs) w projekcie [aplikacji testowej konsoli.](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples)

## <a name="rest-request"></a>Żądanie REST

Aby pobrać link do pobrania Umowa z Klientem Microsoft szablonu:

1. Pobierz metadane umowy dla Umowa z Klientem Microsoft. Należy uzyskać **templateId** Umowa z Klientem Microsoft. Aby uzyskać więcej informacji, zobacz [Get agreement metadata for Umowa z Klientem Microsoft](get-customer-agreement-metadata.md)(Uzyskiwanie metadanych umowy dla Umowa z Klientem Microsoft ).

2. Utwórz żądanie REST, aby pobrać [ **zasób AgreementDocument.**](./agreement-document-resources.md) Przykład można znaleźć w [przykładzie składni](#request-syntax) żądania. Należy określić następujące informacje:

    - **TemplateId** Umowa z Klientem Microsoft.
    - Kraj, do którego ma Umowa z Klientem Microsoft szablon.
    - Język, w którym Umowa z Klientem Microsoft szablon powinien być zlokalizowany.

### <a name="request-syntax"></a>Składnia żądania

Użyj następującej składni żądania dla tego zasobu:

| Metoda | Identyfikator URI żądania |
|--------|---------------------------------------------------------------------|
| GET | [*\{ baseURL \}*](partner-center-rest-urls.md)/v1/agreementtemplates/{identyfikator-szablonu-umowy}/document?language={language}&country={country} HTTP/1.1 |

### <a name="uri-parameters"></a>Parametry URI

W żądaniu można użyć następujących parametrów URI:

| Nazwa                   | Typ   | Wymagane | Opis                                 |
|------------------------|--------|----------|---------------------------------------------|
| identyfikator szablonu umowy  | ciąg | Tak      | Unikatowy identyfikator typu umowy. Możesz uzyskać szablon templateId dla Umowa z Klientem Microsoft, pobierania metadanych umowy dla Umowa z Klientem Microsoft. Aby uzyskać więcej informacji, zobacz [Get agreement metadata for Umowa z Klientem Microsoft](./get-customer-agreement-metadata.md)(Uzyskiwanie metadanych umowy dla Umowa z Klientem Microsoft ). W tym parametrze **jest zróżnicowa wielkość liter.**|
| country                | ciąg | Nie       | Wskazuje kraj, do którego ma zastosowanie szablon umowy. Jeśli parametr nie zostanie *określony,* zapytanie zostanie domyślnie włączone w USA. Aby uzyskać listę obsługiwanych kodów krajów, zapoznaj się [z listą obsługiwanych krajów i języków.](#list-of-supported-countries-and-languages)|
| language               | ciąg | Nie       | Wskazuje język, w którym szablon umowy powinien być zlokalizowany. Zapytanie domyślnie określa wartość *en-US,* jeśli parametr nie został określony lub kod kraju określony w parametrze nie jest obsługiwany dla określonego kraju. Aby uzyskać listę obsługiwanych kodów krajów, zapoznaj [się z listą obsługiwanych krajów i języków.](#list-of-supported-countries-and-languages)|

### <a name="request-headers"></a>Nagłówki żądań

Aby uzyskać więcej informacji, [zobacz Partner Center REST headers (Nagłówki REST).](headers.md)

### <a name="request-body"></a>Treść żądania

Brak.

### <a name="request-example"></a>Przykład żądania

```http
GET https://api.partnercenter.microsoft.com/v1/agreementtemplates/117a77b0-9360-443b-8795-c6dedc750cf9/document?language=en-US&country=US HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 94e4e214-6b06-4fb7-96d1-94d559f9b47f
MS-CorrelationId: ab993325-1605-4cf4-bac4-fb584142a31b
```

## <a name="rest-response"></a>Odpowiedź REST

W przypadku powodzenia ta metoda zwraca [ **zasób AgreementDocument**](./agreement-document-resources.md) w treści odpowiedzi.

Zasób ma właściwość **downloadUri,** która zawiera ciąg adresu URL, którego można użyć do pobrania szablonu umowy. Przy każdym zapytaniu jest zwracany inny link. Ten link wygasa po pięciu minutach.

### <a name="response-success-and-error-codes"></a>Kody powodzenia i błędów odpowiedzi

Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie, oraz dodatkowe informacje o debugowaniu.

Użyj narzędzia śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry. Aby uzyskać pełną listę, zobacz [Partner Center kodów błędów REST.](error-codes.md)

### <a name="response-example"></a>Przykład odpowiedzi

```http
HTTP/1.1 200 OK
Content-Length: 620
Content-Type: application/json
MS-RequestId: 94e4e214-6b06-4fb7-96d1-94d559f9b47f
MS-CorrelationId: ab993325-1605-4cf4-bac4-fb584142a31b
{
    "displayUri":"https://wopihost.int.l2o.microsoft.com/v1/officehost/agreement/files/Preview...",
    "downloadUri":"https://l2oagreementintbn2.blob.core.windows.net/agreementscontainer/Preview...",
    "language":"en-US",
    "country":"US"
}
```

## <a name="list-of-supported-countries-and-languages"></a>Lista obsługiwanych krajów i języków

> [!IMPORTANT]
> Właściwość kodu kraju jest zróżnicowała wielkość liter. Upewnij się, że używasz poprawnej wielkości obudowy określonej w poniższej tabeli.

| Kraj                   | Numer kierunkowy kraju   | Obsługiwane kodów języków |
|------------------------|--------|----------|
| Wyspy alandzkie | Ax | en-US |
| Afganistan | AF | en-US |
| Albania | AL | en-US |
| Algieria | DZ | en-US, fr-FR, en-US |
| Samoa Amerykańskie | AS | en-US |
| Andora | AD | en-US |
| Angola | AO | en-US, pt-PT |
| Anguilla | Sztuczna inteligencja | en-US |
| Antarktyda | Aq | en-US |
| Antigua i Barbuda | AG | en-US |
| Argentyna | AR | en-US, es-ES |
| Armenia | AM | en-US |
| Aruba | Awh | en-US |
| Australia | AU | en-US |
| Austria | AT | en-US, de-DE |
| Azerbejdżan | AZ | en-US |
| Bahamy | BS | en-US |
| Bahrajn | BH | en-US, ar-SA |
| Bangladesz | BD | en-US |
| Barbados | BB | en-US |
| Białoruś | BY | en-US, ru-RU |
| Belgia | BE | en-US, nl-NL |
| Belize | BZ | en-US, es-ES |
| Benin | BJ | en-US |
| Bermudy | Bm | en-US |
| Bhutan | BT | en-US |
| Boliwia | BO | en-US, es-ES |
| Bonaire | Bq | en-US |
| Bośnia i Hercegowina | BA | en-US |
| Botswana | BW | en-US |
| Wyspa Bouveta | Bv | en-US |
| Brazylia | BR | en-US, pt-BR |
| Brytyjskie Terytorium Oceanu Indyjskiego | WE/WY | en-US |
| Brytyjskie Wyspy Dziewicze | VG | en-US |
| Brunei | BN | en-US |
| Bułgaria | BG | en-US, bg-BG |
| Burkina Faso | BF | en-US |
| Burundi | BI | en-US |
| Côte d'Ivoire | CI | en-US, fr-FR |
| Cabo Verde | CV | en-US, pt-PT |
| Kambodża | KH | en-US |
| Kamerun | CM | en-US, fr-FR |
| Kanada | CA | en-US, fr-FR |
| Kajmany | KY | en-US, en-US |
| Republika Środkowoafrykańska | CF | en-US |
| Czad | TD | en-US |
| Chile | CL | en-US, es-ES |
| Wyspa Bożego Narodzenia | CX | en-US |
| Wyspy Kokosowe (Keelinga) | CC | en-US |
| Kolumbia | CO | en-US, es-ES |
| Komory | Km | en-US |
| Kongo (DRK) | CD | en-US |
| Kongo | Cg | en-US |
| Wyspy Cooka | Ck | en-US |
| Kostaryka | CR | en-US, es-ES |
| Chorwacja | HR | en-US, hr-HR |
| Curaçao | Cw | en-US |
| Cypr | CY | en-US |
| Czechy | CZ | en-US, cs-CZ |
| Dania | DK | en-US, da-DK |
| Dżibuti | Dj | en-US |
| Dominika | DM | en-US |
| Dominikana | DO | en-US, es-ES |
| Ekwador | EC | en-US |
| Egipt | EG | en-US, ar-SA |
| Salwador | SV | en-US, es-ES |
| Gwinea Równikowa | Gq | en-US |
| Erytrea | ER | en-US |
| Estonia | EE | en-US, et-EE |
| eSwatini | SZ | en-US |
| Etiopia | ET | en-US |
| Falklandy | Fk | en-US |
| Wyspy Owcze | Fo | en-US |
| Fidżi | FJ | en-US |
| Finlandia | FI | en-US, fi-FI |
| Francja | PW | en-US, fr-FR |
| Gujana Francuska | GF | en-US, fr-FR  |
| Polinezja Francuska | PF | en-US |
| Francuskie Terytoria Południowe i Antarktyczne | Tf | en-US |
| Gabon | Ogólna dostępność | en-US |
| Gambia | GM | en-US |
| Gruzja | GE | en-US |
| Niemcy | DE | en-US, de-DE |
| Ghana | GH | en-US |
| Gibraltar | Gi | en-US |
| Grecja | GR | en-US, el-GR |
| Grenlandia | Gl | en-US |
| Grenada | Gd | en-US |
| Gwadelupa | GP | en-US |
| Guam | GU | en-US |
| Gwatemala | GT | en-US, es-ES |
| Guernsey | Gg | en-US |
| Gwinea | GN | en-US |
| Gwinea Bissau | Gw | en-US |
| Gujana | GY | en-US |
| Haiti | HT | en-US |
| Wyspy Heard i McDonalda | Hm | en-US |
| Honduras | HN | en-US, es-ES |
| SRA Hongkong | HK | en-US, zh-HK |
| Węgry | HU | en-US, hu-HU |
| Islandia | IS | en-US |
| Indie | IN | en-US, hi-IN |
| Indonezja | ID (Identyfikator) | en-US, id-ID |
| Irak | IQ | en-US, ar-SA |
| Irlandia | IE | en-US |
| Wyspa Man | WIADOMOŚĆ BŁYSKAWICZNA | en-US |
| Izrael | IL | en-US, he-IL |
| Włochy | IT | en-US, it-IT |
| Jamajka | JM | en-US |
| Jan Mayen | Xj | en-US |
| Japonia | JP | en-US, ja-JP |
| Jersey | JE | en-US |
| Jordania | JO | en-US, ar-SA |
| Kazachstan | KZ | en-US, kk-KZ |
| Kenia | KE | en-US |
| Kiribati | KI | en-US |
| Korea | KR | en-US, ko-KR |
| Kosowo | Xk | en-US |
| Kuwejt | KW | en-US, ar-SA |
| Kirgistan | KG | en-US, ru-RU |
| Laos | LA | en-US |
| Łotwa | LV | en-US, lv-LV |
| Liban | LB | en-US, ar-SA |
| Lesotho | LS | en-US |
| Liberia | LR | en-US |
| Libia | LY | en-US, ar-SA |
| Liechtenstein | LI | en-US, de-DE |
| Litwa | LT | en-US, lt-LT |
| Luksemburg | LU | en-US, fr-FR |
| SRA Makau | MO | en-US, zh-HK |
| Fca, FYRO | MK | en-US |
| Madagaskar | MG | en-US |
| Malawi | MW | en-US |
| Malezja | MY | en-US, ms-MY |
| Malediwy | MV | en-US |
| Mali | ML | en-US |
| Malta | MT | en-US |
| Wyspy Marshalla | MH | en-US |
| Martynika | MQ | en-US |
| Mauretania | MR | en-US |
| Mauritius | MU | en-US, ar-SA |
| Wyspa Majotta | YT | en-US |
| Meksyk | MX | en-US, es-ES |
| Mikronezja | FM | en-US |
| Mołdawia | MD | en-US, ro-RO |
| Monako | MC | en-US, fr-FR |
| Mongolia | MN | en-US |
| Czarnogóra | ME | en-US |
| Montserrat | MS | en-US |
| Maroko | MA | en-US, fr-FR, en-US |
| Mozambik | MZ | en-US |
| Myanmar | MM | en-US |
| Namibia | NA | en-US |
| Nauru | NR | en-US |
| Nepal | NP | en-US |
| Holandia | NL | en-US, nl-NL |
| Nowa Kaledonia | NC | en-US |
| Nowa Zelandia | NZ | en-US |
| Nikaragua | NI | en-US, es-ES |
| Niger | NE | en-US |
| Nigeria | NG | en-US |
| Niue | NU | en-US |
| Norfolk | Nf | en-US |
| Mariany Północne | MP | en-US |
| Norwegia | NO | en-US, nb-NO |
| Oman | OM | en-US, ar-SA |
| Pakistan | PK | en-US |
| Palau | PW | en-US |
| Autonomia Palestyńska | PS | en-US |
| Panama | PA | en-US, es-ES |
| Papua Nowa Gwinea | Str | en-US |
| Paragwaj | PY | en-US, es-ES |
| Peru | PE | en-US, es-ES |
| Filipiny | PH | en-US |
| Wyspy Pitcairn | Pn | en-US |
| Polska | PL | en-US, pl-PL |
| Portugalia | PT | en-US, pt-PT |
| Portoryko | PR | en-US, en-US |
| Katar | QA | en-US, ar-SA |
| Réunion | RE | en-US |
| Rumunia | RO | en-US, ro-RO |
| Rosja | RU | en-US, ru-RU |
| Rwanda | RW | en-US, fr-FR |
| São Tomé i Prüncipe | SKLEP | en-US, fr-FR |
| Saba | Xs | en-US |
| Saint-Barthélemy | BL | en-US |
| Saint Kitts i Nevis | KN | en-US |
| Saint Lucia | Lc | en-US, en-US |
| Saint-Martin | Mf | en-US, en-US |
| Saint Pierre i Miquelon | PM | en-US |
| Saint Vincent i Grenadyny | VC | en-US |
| Samoa | WS | en-US |
| San Marino | Sm | en-US |
| Arabia Saudyjska | SA | en-US |
| Senegal | SN | en-US, fr-FR |
| Serbia | RS | en-US, sr-Latn-RS, en-US |
| Seszele | SC | en-US |
| Sierra Leone | SL | en-US |
| Singapur | SG | en-US, zh-SG |
| Sint Eustatius | Xe | en-US |
| Sint Maarten | Sx | en-US, en-US |
| Słowacja | SK | en-US, sk-SK |
| Słowenia | SI | en-US, sl-SI |
| Wyspy Salomona | Sb | en-US |
| Somalia | SO | en-US |
| Republika Południowej Afryki | ZA | en-US |
| Georgia Południowa i Sandwich Południowy | Gs | en-US |
| Sudan Południowy | SS | en-US |
| Hiszpania | ES | en-US, es-ES, en-US, en-US |
| Sri Lanka | LK | en-US |
| StRowa, Ascension, Tristan da Cunha | SH | en-US |
| Surinam | SR | en-US |
| Svalbard | Sj | en-US |
| Szwecja | SE | en-US, sv-SE |
| Szwajcaria | CH | en-US, fr-FR, en-US, en-US |
| Tajwan | TW | en-US, zh-HK |
| Tadżykistan | Tj. | en-US |
| Tanzania | TZ | en-US |
| Tajlandia | TH | en-US, th-TH |
| Timor-Leste | TL | en-US |
| Togo | TG | en-US |
| Tokelau | Tk | en-US |
| Tonga | TO | en-US |
| Trinidad i Tobago | TT | en-US |
| Tunezja | TN | en-US, fr-FR, en-US |
| Turcja | TR | en-US, tr-TR |
| Turkmenistan | TM | en-US |
| Wyspy Turks i Caicos | TC | en-US |
| Tuvalu | TV | en-US |
| Stany Zjednoczone Odlying Islands | UM | en-US |
| Wyspy Dziewicze Stanów Zjednoczonych | VI | en-US |
| Uganda | UG | en-US |
| Ukraina | UA | en-US, uk-UA |
| Zjednoczone Emiraty Arabskie | AE | en-US, ar-SA |
| Zjednoczone Królestwo | GB | en-US |
| Stany Zjednoczone | USA | en-US |
| Urugwaj | UY | en-US, es-ES |
| Uzbekistan | UZ | en-US, ru-RU |
| Vanuatu | Vu | en-US |
| Watykan | VA | en-US |
| Wenezuela | VE | en-US, es-ES |
| Wietnam | VN | en-US, vi-VN |
| Wallis i Ichuna | WF | en-US |
| Jemen | Ye | en-US, ar-SA |
| Zambia | ZM | en-US |
| Zimbabwe | ZW | en-US |
