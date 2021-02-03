---
title: Pobierz link do pobierania dla szablonu umowy klienta firmy Microsoft
description: Pobierz link pobierania dla szablonu umowy klienta firmy Microsoft.
ms.date: 02/12/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: cychua
ms.author: cychua
ms.openlocfilehash: 8c794d264ad64a42fa6ca823ddfc3841248c01cd
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/08/2020
ms.locfileid: "97767990"
---
# <a name="get-a-download-link-for-the-microsoft-customer-agreement-template"></a>Pobierz link do pobierania dla szablonu umowy klienta firmy Microsoft

**Dotyczy:**

- Centrum partnerskie

Zasób **AgreementDocument** jest obecnie obsługiwany przez centrum partnerskie tylko w *chmurze publicznej firmy Microsoft*. Ten zasób nie ma zastosowania do:

- Centrum partnerskie obsługiwane przez firmę 21Vianet
- Centrum partnerskie dla Microsoft Cloud Niemcy
- Centrum partnerskie Microsoft Cloud for US Government

W tym artykule opisano, jak uzyskać link umożliwiający pobranie szablonu umowy klienta firmy Microsoft na podstawie kraju i języka klienta.

## <a name="prerequisites"></a>Wymagania wstępne

- W przypadku korzystania z zestawu SDK platformy .NET w programie Partner Center wymagany jest program w wersji 1,14 lub nowszej.

- Poświadczenia zgodnie z opisem w temacie [uwierzytelnianie w centrum partnerskim](./partner-center-authentication.md). Ten scenariusz obsługuje tylko uwierzytelnianie aplikacji i użytkowników.

- Kraj klienta, do którego ma zastosowanie szablon umowy klienta firmy Microsoft.

- Język, w którym należy lokalizować szablon umowy klienta firmy Microsoft.

> [!IMPORTANT]
>
> - Umowa dla klientów firmy Microsoft jest specyficzna dla kraju. Gdy żądasz linku do pobrania szablonu umowy klienta firmy Microsoft, pamiętaj o określeniu odpowiedniego kraju na podstawie lokalizacji klienta. lub listę obsługiwanych krajów zapoznaj się z [listą obsługiwanych krajów i języków](#list-of-supported-countries-and-languages).
>
> - W przypadku niektórych krajów umowa klienta firmy Microsoft jest dostępna w wielu językach. Aby zapewnić najlepszą obsługę klienta, wybierz język, który najlepiej odpowiada potrzebom klientów. Aby uzyskać listę obsługiwanych języków, zapoznaj się z [listą obsługiwanych krajów i języków](#list-of-supported-countries-and-languages).
> - Ta metoda jest obsługiwana tylko przez umowę klienta firmy Microsoft.

## <a name="net"></a>.NET

Aby pobrać link do pobrania szablonu umowy klienta firmy Microsoft:

1. Pobierz metadane umowy dla umowy klienta firmy Microsoft. Musisz uzyskać **TemplateID** umowy klienta firmy Microsoft. Aby uzyskać więcej informacji, zobacz [Pobierz metadane umowy dla umowy klienta firmy Microsoft](get-customer-agreement-metadata.md).

   ```csharp
   // IAggregatePartner partnerOperations;

   string agreementType = "MicrosoftCustomerAgreement";

   AgreementMetaData microsoftCustomerAgreementDetails = partnerOperations.AgreementDetails.   ByAgreementType(agreementType).Get().Items.Single();
   ```

2. Użyj kolekcji IAggregatePartner. AgreementTemplates.

3. Wywołaj metodę **ById** i określ **TemplateID** umowy klienta firmy Microsoft.

4. Pobierz Właściwość **dokumentu** .

5. Wywołaj metodę **ByCountry** i określ kraj klienta, do którego ma zastosowanie szablon umowy. Jeśli nie określono metody, zapytanie jest domyślnie ustawiane jako *US* . Aby zapoznać się z listą obsługiwanych kodów krajów, zapoznaj się z [listą obsługiwanych krajów i języków](#list-of-supported-countries-and-languages). W tej metodzie jest **rozróżniana wielkość** liter.

6. Wywołaj metodę **ByLanguage** i określ język, w którym szablon umowy powinien być zlokalizowany. Jeśli metoda nie została określona lub określony kod kraju nie jest obsługiwany dla określonego kraju, zapytanie jest domyślnie ustawiane jako *en-us* . Aby uzyskać listę obsługiwanych kodów języka, zapoznaj się z [listą obsługiwanych krajów i języków](#list-of-supported-countries-and-languages).

7. Wywołaj metodę **Get** lub **GetAsync** .

   ```csharp
   // IAggregatePartner partnerOperations;

   string customerCountry = "US";

   string languageForLocalization = "en-US";

   var agreementDocument = partnerOperations.   AgreementTemplates.ById   (microsoftCustomerAgreementDetails.   TemplateId).Document.ByCountry   (customerCountry).ByLanguage   (languageForLocalization).Get();
   ```

Pełny przykład można znaleźć w klasie [GetAgreementDetails](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples/blob/master/Source/Partner%20Center%20SDK%20Samples/Agreements/GetAgreementDetails.cs) z projektu [aplikacji testowej konsoli](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples) .

## <a name="rest-request"></a>Żądanie REST

Aby pobrać link do pobrania szablonu umowy klienta firmy Microsoft:

1. Pobierz metadane umowy dla umowy klienta firmy Microsoft. Musisz uzyskać **TemplateID** umowy klienta firmy Microsoft. Aby uzyskać więcej informacji, zobacz [Pobierz metadane umowy dla umowy klienta firmy Microsoft](get-customer-agreement-metadata.md).

2. Utwórz żądanie REST w celu pobrania zasobu [ **AgreementDocument**](./agreement-document-resources.md). Aby zapoznać się z przykładem, zobacz przykład [składni żądania](#request-syntax) . Należy określić następujące informacje:

    - **TemplateID** umowy klienta firmy Microsoft.
    - Kraj, do którego ma zastosowanie szablon umowy klienta firmy Microsoft.
    - Język, w którym należy lokalizować szablon umowy klienta firmy Microsoft.

### <a name="request-syntax"></a>Składnia żądania

Użyj następującej składni żądania dla tego zasobu:

| Metoda | Identyfikator URI żądania |
|--------|---------------------------------------------------------------------|
| GET | [*\{ baseURL \}*](partner-center-rest-urls.md)/V1/agreementtemplates/{Agreement-Template-ID}/Document? Language = {Language} &Country = {Country} http/1.1 |

### <a name="uri-parameters"></a>Parametry identyfikatora URI

Z żądaniem można użyć następujących parametrów URI:

| Nazwa                   | Typ   | Wymagane | Opis                                 |
|------------------------|--------|----------|---------------------------------------------|
| Umowa — identyfikator szablonu  | ciąg | Tak      | Unikatowy identyfikator typu umowy. Możesz uzyskać templateId dla umowy klienta Microsoft, pobierając metadane umowy dla umowy klienta firmy Microsoft. Aby uzyskać więcej informacji, zobacz [Pobierz metadane umowy dla umowy klienta firmy Microsoft](./get-customer-agreement-metadata.md). W tym parametrze jest **rozróżniana wielkość** liter.|
| country                | ciąg | Nie       | Wskazuje kraj, do którego ma zastosowanie szablon umowy. Jeśli parametr nie jest określony, zapytanie jest domyślnie ustawiane jako *US* . Aby zapoznać się z listą obsługiwanych kodów krajów, zapoznaj się z [listą obsługiwanych krajów i języków](#list-of-supported-countries-and-languages).|
| language               | ciąg | Nie       | Wskazuje język, w którym szablon umowy powinien być zlokalizowany. Jeśli parametr nie jest określony lub określony przez kod kraju in't jest obsługiwany dla danego kraju, zapytanie jest domyślnie ustawiane jako *en-us* . Listę obsługiwanych kodów krajów można znaleźć na [liście obsługiwanych krajów i języków](#list-of-supported-countries-and-languages).|

### <a name="request-headers"></a>Nagłówki żądań

Aby uzyskać więcej informacji, zobacz [nagłówki REST Centrum partnerskiego](headers.md).

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

Jeśli to się powiedzie, metoda zwraca [zasób **AgreementDocument**](./agreement-document-resources.md) w treści odpowiedzi.

Zasób ma właściwość **downloadUri** , która zawiera ciąg adresu URL, którego można użyć do pobrania szablonu umowy. Za każdym razem, gdy wykonujesz zapytanie, zwracany jest inny link. Ten link wygasa po pięciu minutach.

### <a name="response-success-and-error-codes"></a>Kody sukcesu i błędów odpowiedzi

Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie i dodatkowe informacje debugowania.

Użyj narzędzia do śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry. Aby uzyskać pełną listę, zobacz [kody błędów REST centrum partnera](error-codes.md).

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
> W właściwości kod kraju jest rozróżniana wielkość liter. Upewnij się, że używasz poprawnej wielkości liter podanej w poniższej tabeli.

| Kraj                   | Numer kierunkowy kraju   | Obsługiwane kody języka |
|------------------------|--------|----------|
| Wyspy Åland | OŚ | en-US |
| Afganistan | AF | en-US |
| Albania | AL | en-US |
| Algieria | DZ | EN-US, fr-FR, en-US |
| Samoa Amerykańskie | AS | en-US |
| Andora | AD | en-US |
| Angola | AO | EN-US, pt-PT |
| Anguilla | Sztuczna inteligencja | en-US |
| Antarktyda | AQ | en-US |
| Antigua i Barbuda | AG | en-US |
| Argentyna | AR | pl-US, es-ES |
| Armenia | AM | en-US |
| Aruba | AW | en-US |
| Australia | AU | en-US |
| Austria | AT | EN-US, de-DE |
| Azerbejdżan | AZ | en-US |
| Bahamy | BS | en-US |
| Bahrajn | BH | EN-US, ar-SA |
| Bangladesz | BD | en-US |
| Barbados | BB | en-US |
| Białoruś | BY | pl-US, ru-RU |
| Belgia | BE | EN-US, NL-NL |
| Belize | BZ | pl-US, es-ES |
| Benin | BJ | en-US |
| Bermudy | BM | en-US |
| Bhutan | BT | en-US |
| Boliwia | BO | pl-US, es-ES |
| Bonaire | BQ | en-US |
| Bośnia i Hercegowina | BA | en-US |
| Botswana | BW | en-US |
| Wyspa Bouveta | BV | en-US |
| Brazylia | BR | EN-US, pt-BR |
| Brytyjskie Terytorium Oceanu Indyjskiego | WE/WY | en-US |
| Brytyjskie Wyspy Dziewicze | VG | en-US |
| Brunei | BN | en-US |
| Bułgaria | BG | EN-US, BG-BG |
| Burkina Faso | BF | en-US |
| Burundi | BI | en-US |
| Côte d'Ivoire | CI | EN-US, fr — FR |
| Cabo Verde | CV | EN-US, pt-PT |
| Kambodża | KH | en-US |
| Kamerun | CM | EN-US, fr — FR |
| Kanada | CA | EN-US, fr — FR |
| Kajmany | KY | EN-US, en-US |
| Republika Środkowoafrykańska | CF | en-US |
| Czad | TD | en-US |
| Chile | CL | pl-US, es-ES |
| Wyspa Bożego Narodzenia | CX | en-US |
| Wyspy Kokosowe (Keelinga) | CC | en-US |
| Kolumbia | CO | pl-US, es-ES |
| Komory | KILOMETR | en-US |
| Kongo (DRK) | CD | en-US |
| Kongo | CG | en-US |
| Wyspy Cooka | Wkręt | en-US |
| Kostaryka | CR | pl-US, es-ES |
| Chorwacja | HR | pl-US, HR-HR |
| Curaçao | CW | en-US |
| Cypr | CY | en-US |
| Czechia | CZ | EN-US, CS — CZ |
| Dania | DK | EN-US, da-DK |
| Dżibuti | DJ | en-US |
| Dominika | DM | en-US |
| Dominikana | DO | pl-US, es-ES |
| Ekwador | EC | en-US |
| Egipt | EG | EN-US, ar-SA |
| Salwador | SV | pl-US, es-ES |
| Gwinea Równikowa | GQ | en-US |
| Erytrea | ER | en-US |
| Estonia | EE | EN-US, et-EE |
| eSwatini | SZ | en-US |
| Etiopia | ET | en-US |
| Falklandy | OBCEGO | en-US |
| Wyspy Owcze | CZCIONKI | en-US |
| Fidżi | FJ | en-US |
| Finlandia | FI | pl-US, fi-FI |
| Francja | PW | EN-US, fr — FR |
| Gujana Francuska | GF | EN-US, fr — FR  |
| Polinezja Francuska | PF | en-US |
| Francuskie Terytoria Południowe i Antarktyczne | TF | en-US |
| Gabon | Ogólna dostępność | en-US |
| Gambia | GM | en-US |
| Gruzja | GE | en-US |
| Niemcy | DE | EN-US, de-DE |
| Ghana | GH | en-US |
| Gibraltar | GI | en-US |
| Grecja | GR | pl-US, El-GR |
| Grenlandia | GL | en-US |
| Grenada | GD | en-US |
| Gwadelupa | GP | en-US |
| Guam | GU | en-US |
| Gwatemala | GT | pl-US, es-ES |
| Guernsey | GG | en-US |
| Gwinea | GN | en-US |
| Gwinea Bissau | GW | en-US |
| Gujana | GY | en-US |
| Haiti | HT | en-US |
| Wyspy Heard i McDonalda | HM | en-US |
| Honduras | HN | pl-US, es-ES |
| SRA Hongkong | HK | pl-US, zh-HK |
| Węgry | HU | EN-US, HU — Węgry |
| Islandia | IS | en-US |
| Indie | IN | pl-US, Hi-IN |
| Indonezja | ID (Identyfikator) | pl-US, identyfikator ID |
| Irak | IQ | EN-US, ar-SA |
| Irlandia | IE | en-US |
| Wyspa Man | WIADOMOŚĆ BŁYSKAWICZNA | en-US |
| Izrael | IL | pl-US, IT-IL |
| Włochy | IT | EN-US, IT |
| Jamajka | JM | en-US |
| Jan Mayen | XJ | en-US |
| Japonia | JP | EN-US, ja-JP |
| Jersey | JE | en-US |
| Jordania | JO | EN-US, ar-SA |
| Kazachstan | KZ | EN-US, KK — KZ |
| Kenia | KE | en-US |
| Kiribati | KI | en-US |
| Korea | KR | EN-US, Ko-KR |
| Kosowo | XK | en-US |
| Kuwejt | KW | EN-US, ar-SA |
| Kirgistan | KG | pl-US, ru-RU |
| Laos | LA | en-US |
| Łotwa | LV | pl-US, LV — LV |
| Liban | LB | EN-US, ar-SA |
| Lesotho | LS | en-US |
| Liberia | LR | en-US |
| Libia | LY | EN-US, ar-SA |
| Liechtenstein | LI | EN-US, de-DE |
| Litwa | LT | EN-US, lt-LT |
| Luksemburg | LU | EN-US, fr — FR |
| SRA Makau | MO | pl-US, zh-HK |
| Macedonia, BJR | MK | en-US |
| Madagaskar | MG | en-US |
| Malawi | MW | en-US |
| Malezja | MY | pl-US, MS — MY |
| Malediwy | MV | en-US |
| Mali | ML | en-US |
| Malta | MT | en-US |
| Wyspy Marshalla | MH | en-US |
| Martynika | MQ | en-US |
| Mauretania | MR | en-US |
| Mauritius | MU | EN-US, ar-SA |
| Wyspa Majotta | YT | en-US |
| Meksyk | MX | pl-US, es-ES |
| Mikronezja | FM | en-US |
| Mołdawia | MD | pl-US, RO-RO |
| Monako | MC | EN-US, fr — FR |
| Mongolia | MN | en-US |
| Czarnogóra | ME | en-US |
| Montserrat | MS | en-US |
| Maroko | MA | EN-US, fr-FR, en-US |
| Mozambik | MZ | en-US |
| Myanmar | MM | en-US |
| Namibia | Nie dotyczy | en-US |
| Nauru | NR | en-US |
| Nepal | NP | en-US |
| Holandia | NL | EN-US, NL-NL |
| Nowa Kaledonia | NC | en-US |
| Nowa Zelandia | NZ | en-US |
| Nikaragua | NI | pl-US, es-ES |
| Niger | NE | en-US |
| Nigeria | NG | en-US |
| Niue | NU | en-US |
| Norfolk | OZNACZONA | en-US |
| Mariany Północne | MP | en-US |
| Norwegia | NO | pl-US, NB-NO |
| Oman | OM | EN-US, ar-SA |
| Pakistan | PK | en-US |
| Palau | PW | en-US |
| Autonomia Palestyńska | PS | en-US |
| Panama | PA | pl-US, es-ES |
| Papua Nowa Gwinea | STRONY | en-US |
| Paragwaj | PY | pl-US, es-ES |
| Peru | PE | pl-US, es-ES |
| Filipiny | PH | en-US |
| Wyspy Pitcairn | NC | en-US |
| Polska | PL | pl-US, pl-PL |
| Portugalia | PT | EN-US, pt-PT |
| Portoryko | PR | EN-US, en-US |
| Katar | QA | EN-US, ar-SA |
| Réunion | RE | en-US |
| Rumunia | RO | pl-US, RO-RO |
| Rosja | RU | pl-US, ru-RU |
| Rwanda | RW | EN-US, fr — FR |
| Wyspy Świętego Tomasza i Książęca | SKLEP | EN-US, fr — FR |
| Saba | XS | en-US |
| Saint-Barthélemy | BL | en-US |
| Saint Kitts i Nevis | KN | en-US |
| Saint Lucia | LC | EN-US, en-US |
| Saint-Martin | CZĘSTOTLIWOŚCI | EN-US, en-US |
| Saint Pierre i Miquelon | PM | en-US |
| Saint Vincent i Grenadyny | VC | en-US |
| Samoa | WS | en-US |
| San Marino | SPRZEDAŻY | en-US |
| Arabia Saudyjska | SA | en-US |
| Senegal | SN | EN-US, fr — FR |
| Serbia | RS | pl-US, sr-latn-RS, en-US |
| Seszele | SC | en-US |
| Sierra Leone | SL | en-US |
| Singapur | SG | pl-US, zh-SG |
| Sint Eustatius | HASŁA | en-US |
| Sint Maarten | SX | EN-US, en-US |
| Słowacja | SK | EN-US, SK-SK |
| Słowenia | SI | EN-US, SL-SI |
| Wyspy Salomona | SB | en-US |
| Somalia | SO | en-US |
| Republika Południowej Afryki | ZA | en-US |
| Georgia Południowa i Sandwich Południowy | GS | en-US |
| Sudan Południowy | SS | en-US |
| Hiszpania | ES | pl-US, es-ES, en-US, en-US |
| Sri Lanka | LK | en-US |
| Święta Helena, Wyspa Wniebowstąpienia, Tristan da Cunha | SH | en-US |
| Surinam | SR | en-US |
| Svalbard | SJ | en-US |
| Szwecja | SE | pl-US, SV — SE |
| Szwajcaria | CH | EN-US, fr-FR, en-US, en-US |
| Tajwan | TW | pl-US, zh-HK |
| Tadżykistan | TJ | en-US |
| Tanzania | TZ | en-US |
| Tajlandia | TH | EN-US, th-TH |
| Timor-Leste | TL | en-US |
| Togo | TG | en-US |
| Tokelau | TK | en-US |
| Tonga | TO | en-US |
| Trinidad i Tobago | TT | en-US |
| Tunezja | TN | EN-US, fr-FR, en-US |
| Turcja | TR | EN-US, TR-TR |
| Turkmenistan | TM | en-US |
| Wyspy Turks i Caicos | TC | en-US |
| Tuvalu | TV | en-US |
| Odległe wyspy Stanów Zjednoczonych | UM | en-US |
| Wyspy Dziewicze Stanów Zjednoczonych | VI | en-US |
| Uganda | UG | en-US |
| Ukraina | UA | pl-US, UK-UA |
| Zjednoczone Emiraty Arabskie | AE | EN-US, ar-SA |
| Zjednoczone Królestwo | GB | en-US |
| Stany Zjednoczone | USA | en-US |
| Urugwaj | UY | pl-US, es-ES |
| Uzbekistan | UZ | pl-US, ru-RU |
| Vanuatu | VU | en-US |
| Watykan | VA | en-US |
| Wenezuela | VE | pl-US, es-ES |
| Wietnam | VN | EN-US, VI-VN |
| Wallis i Futuna | WF | en-US |
| Jemen | YE | EN-US, ar-SA |
| Zambia | ZM | en-US |
| Zimbabwe | ZW | en-US |
