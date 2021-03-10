---
title: Języki obsługiwane przez Centrum partnerskie i ustawienia regionalne
description: Lista elementów ISO2 i ISO3 obsługiwanych lokalnie dla Centrum partnerskiego.
ms.date: 12/03/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: cychua
ms.author: cychua
ms.openlocfilehash: d486eed96586eb2577577eac44fa9e866479e825
ms.sourcegitcommit: 9bc35836b389fdf083b278128a2e9ec994919f1c
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 03/10/2021
ms.locfileid: "102532842"
---
# <a name="partner-center-supported-languages-and-locales"></a>Języki obsługiwane przez Centrum partnerskie i ustawienia regionalne

**Dotyczy**

- Centrum partnerskie
- Centrum partnerskie obsługiwane przez firmę 21Vianet
- Centrum partnerskie dla Microsoft Cloud Niemcy
- Centrum partnerskie Microsoft Cloud for US Government

Niektóre interfejsy API Centrum partnerskiego wymagają wartości wskazującej ustawienia regionalne, kraj lub region. Na przykład [nagłówek REST Centrum partnerskiego](headers.md) X-locale wymaga wartości często w formacie "Country-US" ("en-pl" wskazuje "angielski-Stany Zjednoczone").

W zarządzanym interfejsie API Centrum partnerskiego — Klasa [CountryValidationRules/dotnet/API/Microsoft. Store. partnercenter. models. CountryValidationRules. CountryValidationRules) oraz [OfferCategory. locale/dotnet/API/Microsoft. Store. partnercenter. models. offer. OfferCategory. locales), [ServiceRequest. CountryCode/dotnet/API/Microsoft. Store. partnercenter. models. servicerequests. ServiceRequest. CountryCode), lub [CustomerBillingProfile. Culture/dotnet/API/Microsoft. Store. partnercenter. models. Customers. CustomerBillingProfile. Culture), właściwości wymagają wartości ciągów wskazujących język lub kraj/region (w postaci kodu języka ISO2 lub ISO3 kod kraju/regionu), ustawienia regionalne, lub kultury (identyfikator języka połączony z kodem kraju/regionu).

Poniższa tabela zawiera listę kultur i kody krajów Międzynarodowej Organizacji Normalizacyjnej (ISO), które są obsługiwane przez interfejsy API Centrum partnerskiego.

| Kraj/region                           | ISO alpha 2 — kod kraju | ISO Alpha 3 — kod kraju | Obsługiwane kultury                  |
|------------------------------------------|--------------------------|--------------------------|---------------------------------------|
| Afganistan                              | AF                       | AFG                      | PS-AF/pl-US                         |
| Wyspy Åland                            | OŚ                       | ROZPORZĄDZENIA                      | SV — SE/pl-US                         |
| Albania                                  | AL                       | ALB                      | kW-AL/pl-US                         |
| Algieria                                  | DZ                       | DZA                      | AR-DZ/pl-US                         |
| Samoa Amerykańskie                           | AS                       | ASM                      | en-US                                 |
| Andora                                  | AD                       | AND                      | CA-ES/pl-US                         |
| Angola                                   | AO                       | TEMU                      | pt-PT/pl-US                         |
| Anguilla                                 | Sztuczna inteligencja                       | AIA                      | en-US                                 |
| Antarktyda                               | AQ                       | ANE                      | en-US                                 |
| Antigua i Barbuda                      | AG                       | ATG                      | en-US                                 |
| Argentyna                                | AR                       | ARG                      | ES-AR/pl-US                         |
| Armenia                                  | AM                       | ARM                      | HY — AM/pl                         |
| Aruba                                    | AW                       | ABW                      | NL-NL/pl-US                         |
| Australia                                | AU                       | JEDNOSTEK analizy                      | en-AU/pl-US                         |
| Austria                                  | AT                       | AUT                      | de-AT/pl-US                         |
| Azerbejdżan                               | AZ                       | AZE                      | az-Latn-AZ/pl-US                    |
| Bahamy                                  | BS                       | BHS                      | pl-GB/pl-US                         |
| Bahrajn                                  | BH                       | BHR                      | AR-BH/pl-US                         |
| Bangladesz                               | BD                       | BGD                      | mld USD — BD/pl                         |
| Barbados                                 | BB                       | BRB                      | pl-GB/pl-US                         |
| Białoruś                                  | BY                       | BLR                      | przypadaj na/pl-US                         |
| Belgia                                  | BE                       | ETYKIETY                      | fr-należy/NL-PL/EN-US                 |
| Belize                                   | BZ                       | BLZ                      | EN-BZ/en-US                         |
| Benin                                    | BJ                       | BEN                      | fr — FR/pl-US                         |
| Bermudy                                  | BM                       | BMU                      | pl-GB/pl-US                         |
| Bhutan                                   | BT                       | BTN                      | en-US                                 |
| Boliwia                                  | BO                       | BOL                      | ES — BO/pl-US                         |
| Bonaire                                  | BQ                       | BES                      | NL-NL/pl-US                         |
| Bośnia i Hercegowina                   | BA                       | BIH                      | BS-Latn-BA/pl-US                    |
| Botswana                                 | BW                       | BWA                      | pl-GB/pl-US                         |
| Wyspa Bouveta                            | BV                       | BVT                      | NB — NO/pl-US                         |
| Brazylia                                   | BR                       | BRA                      | pt-BR/pl-US                         |
| Brytyjskie Terytorium Oceanu Indyjskiego           | WE/WY                       | IOT                      | en-US                                 |
| Brytyjskie Wyspy Dziewicze                   | VG                       | VGB                      | en-US                                 |
| Brunei                                   | BN                       | BRN                      | MS-mld USD/pl-US                         |
| Bułgaria                                 | BG                       | BGR                      | BG — BG/en-US                         |
| Burkina Faso                             | BF                       | BFA                      | fr — FR/pl-US                         |
| Burundi                                  | BI                       | BDI                      | fr — FR/pl-US                         |
| Cabo Verde                               | CV                       | NOMENKLATUR                      | pt-CV/pl-US                         |
| Kambodża                                 | KH                       | KHM                      | km-KH/pl-US                         |
| Kamerun                                 | CM                       | CMR                      | fr — FR/pl-US                         |
| Kanada                                   | CA                       | MOŻE                      | fr — CA/pl-US                         |
| Kajmany                           | KY                       | CYM                      | pl-GB/pl-US                         |
| Republika Środkowoafrykańska                 | CF                       | CAF                      | fr — FR/pl-US                         |
| Czad                                     | TD                       | TCD                      | fr — FR/pl-US                         |
| Chile                                    | CL                       | CHL                      | ES — CL/pl-US                         |
| Chiny                                    | CN                       | CHN                      | zh-CN/pl-US                         |
| Wyspa Bożego Narodzenia                         | CX                       | CXR                      | en-US                                 |
| Wyspy Kokosowe (Keelinga)                  | CC                       | CCK                      | en-US                                 |
| Kolumbia                                 | CO                       | KOLUMNA                      | ES — współpracujące z nami                         |
| Komory                                  | KILOMETR                       | Model COM                      | fr — FR/pl-US                         |
| Kongo                                    | CG                       | KOŁO zębate                      | fr — FR/pl-US                         |
| Kongo (DRK)                              | CD                       | COD                      | fr — FR/pl-US                         |
| Wyspy Cooka                             | Wkręt                       | COK                      | en-US                                 |
| Kostaryka                               | CR                       | CRI                      | ES — CR/pl-US                         |
| Côte d'Ivoire                            | CI                       | CIV                      | fr — FR/pl-US                         |
| Chorwacja                                  | HR                       | HRV                      | HR-HR/pl-US                         |
| Curaçao                                  | CW                       | CUW                      | NL-NL/pl-US                         |
| Cypr                                   | CY                       | CYP                      | El-GR/pl-US                         |
| Czechia                                  | CZ                       | CZE                      | CS — CZ/pl-US                         |
| Dania                                  | DK                       | DNK                      | da — DK/pl-US                         |
| Dżibuti                                 | DJ                       | DJI                      | fr — FR/pl-US                         |
| Dominika                                 | DM                       | Narzędzie DMA                      | en-US                                 |
| Dominikana                       | DO                       | DOM                      | ES — Zrób/en-US                         |
| Ekwador                                  | EC                       | NOSZĄC                      | ES — we/pl — US                         |
| Egipt                                    | EG                       | EGY                      | AR-EG/en-US                         |
| Salwador                              | SV                       | SLV                      | ES — SV/pl-US                         |
| Gwinea Równikowa                        | GQ                       | GNQ                      | es-ES/pl-US                         |
| Erytrea                                  | ER                       | ERI                      | ar-SA/pl-US                         |
| Estonia                                  | EE                       | EST                      | et-EE/pl-US                         |
| eSwatini                                 | SZ                       | SWZ                      | en-US                                 |
| Etiopia                                 | ET                       | ETH                      | am-ET/pl-US                         |
| Falklandy                         | OBCEGO                       | FLK                      | en-US                                 |
| Wyspy Owcze                            | CZCIONKI                       | ZAPIS                      | FO-FO/en-US                         |
| Fidżi                                     | FJ                       | FJI                      | pl-GB/pl-US                         |
| Finlandia                                  | FI                       | FIN                      | fi-FI/SV-FI/pl-US                 |
| Francja                                   | PW                       | FRA                      | fr — FR/pl-US                         |
| Gujana Francuska                            | GF                       | GUF                      | fr — FR/pl-US                         |
| Polinezja Francuska                         | PF                       | PYF                      | fr — FR/pl-US                         |
| Francuskie Terytoria Południowe i Antarktyczne              | TF                       | ATF                      | fr — FR/pl-US                         |
| Gabon                                    | Ogólna dostępność                       | GAB                      | fr — FR/pl-US                         |
| Gambia                                   | GM                       | GMB                      | en-US                                 |
| Gruzja                                  | GE                       | GEOGRAFICZNIE                      | ka-GE/pl-US                         |
| Niemcy                                  | DE                       | DEU                      | de-DE/pl-US                         |
| Ghana                                    | GH                       | GHA                      | pl-GB/pl-US                         |
| Gibraltar                                | GI                       | GIB                      | en-US                                 |
| Grecja                                   | GR                       | GRC                      | El-GR/pl-US                         |
| Grenlandia                                | GL                       | GLOBALNEJ                      | da — DK/pl-US                         |
| Grenada                                  | GD                       | GRD                      | en-US                                 |
| Gwadelupa                               | GP                       | ORGANU                      | fr — FR/pl-US                         |
| Guam                                     | GU                       | GUMA                      | en-US                                 |
| Gwatemala                                | GT                       | GTM                      | ES-GT/pl-US                         |
| Guernsey                                 | GG                       | GGY                      | en-US                                 |
| Gwinea                                   | GN                       | ĄTEK                      | fr — FR/pl-US                         |
| Gwinea Bissau                            | GW                       | GNB                      | pt-PT/pl-US                         |
| Gujana                                   | GY                       | GUY                      | en-US                                 |
| Haiti                                    | HT                       | HTI                      | fr — FR/pl-US                         |
| Wyspy Heard i McDonalda        | HM                       | HMD                      | en-US                                 |
| Honduras                                 | HN                       | HND                      | ES — HN/pl-US                         |
| SRA Hongkong                            | HK                       | HKG                      | zh-HK/pl-US                         |
| Węgry                                  | HU                       | HUN                      | HU — Węgry/en-US                         |
| Islandia                                  | IS                       | JEST zwracany                      | IS-IS/pl-US                         |
| Indie                                    | IN                       | IND                      | pl-IN/Hi-IN/pl-US                 |
| Indonezja                                | ID (Identyfikator)                       | IDN                      | ID-ID/pl-US                         |
| Irak                                     | IQ                       | Sterowanie                      | AR-IQ/pl-US                         |
| Irlandia                                  | IE                       | IRL                      | EN-IE/pl-US                         |
| Wyspa Man                              | WIADOMOŚĆ BŁYSKAWICZNA                       | IMN                      | en-US                                 |
| Izrael                                   | IL                       | ISR                      | IT-IL/pl-US                         |
| Włochy                                    | IT                       | ITA                      | IT/en-US                         |
| Jamajka                                  | JM                       | Cięcie                      | pl-JM/pl-US                         |
| Jan Mayen                                | XJ                       | XJA                      | NB — NO/pl-US                         |
| Japonia                                    | JP                       | JPN                      | ja-JP/pl-US                         |
| Jersey                                   | JE                       | JEY                      | en-US                                 |
| Jordania                                   | JO                       | JOR                      | AR — JO/en-US                         |
| Kazachstan                               | KZ                       | KAZ                      | KK-KZ/pl-US                         |
| Kenia                                    | KE                       | Krzysztof                      | SW — KE/en-US                         |
| Kiribati                                 | KI                       | KIR                      | en-US                                 |
| Korea                                    | KR                       | KOR                      | Ko — KR/en-US                         |
| Kosowo                                   | XK                       | XKS                      | en-US                                 |
| Kuwejt                                   | KW                       | KWT                      | AR-KW/pl-US                         |
| Kirgistan                               | KG                       | KGZ                      | KY-KG/pl-US                         |
| Laos                                     | LA                       | -                      | Lo-LA/en-US                         |
| Łotwa                                   | LV                       | LVA                      | LV — LV/pl-US                         |
| Liban                                  | LB                       | LBN                      | AR-LB/pl-US                         |
| Lesotho                                  | LS                       | LSO                      | en-US                                 |
| Liberia                                  | LR                       | LBR                      | en-US                                 |
| Libia                                    | LY                       | LBY                      | AR-LY/pl-US                         |
| Liechtenstein                            | LI                       | SPOCZYWA                      | de-LI/pl-US                         |
| Litwa                                | LT                       | LTU                      | lt — LT/pl-US                         |
| Luksemburg                               | LU                       | AŻ                      | de-LU/fr-LU/pl-US                 |
| SRA Makau                                | MO                       | Komputery                      | zh-MO/pl-US                         |
| Macedonia, BJR                          | MK                       | MKD                      | mk-MK/pl-US                         |
| Madagaskar                               | MG                       | MDG                      | fr — FR/pl-US                         |
| Malawi                                   | MW                       | MWI                      | en-US                                 |
| Malezja                                 | MY                       | MYS                      | pl — MY/pl-US                         |
| Malediwy                                 | MV                       | MDV                      | DV-MV/pl-US                         |
| Mali                                     | ML                       | MLI                      | fr — FR/pl-US                         |
| Malta                                    | MT                       | MLT                      | MT-MT/pl-US                         |
| Wyspy Marshalla                         | MH                       | MHL                      | en-US                                 |
| Martynika                               | MQ                       | MTQ                      | fr — FR/pl-US                         |
| Mauretania                               | MR                       | PLIK                      | ar-SA/pl-US                         |
| Mauritius                                | MU                       | MUS                      | pl-GB/pl-US                         |
| Wyspa Majotta                                  | YT                       | MYT                      | fr — FR/pl-US                         |
| Meksyk                                   | MX                       | MEX                      | es — MX/pl-US                         |
| Mikronezja                               | FM                       | FSM                      | en-US                                 |
| Mołdawia                                  | MD                       | MDA                      | RO-RO/pl-US                         |
| Monako                                   | MC                       | MCO                      | fr-MC/pl-US                         |
| Mongolia                                 | MN                       | MNG                      | MN-MN/pl-US                         |
| Czarnogóra                               | ME                       | MNE                      | sr-latn-ME/pl-US                    |
| Montserrat                               | MS                       | MSR                      | en-US                                 |
| Maroko                                  | MA                       | MAR                      | AR — MA/pl-US                         |
| Mozambik                               | MZ                       | MOZ                      | pt-PT                                 |
| Myanmar                                  | MM                       | MMR                      | en-US                                 |
| Namibia                                  | NA                       | Wietnam                      | pl-GB/pl-US                         |
| Nauru                                    | NR                       | NRU                      | en-US                                 |
| Nepal                                    | NP                       | NPL                      | ne — NP./en-US                         |
| Antyle Holenderskie                     | WSKAZANI                       | ANT                      | en-US                                 |
| Holandia,                         | NL                       | NLD                      | NL-NL/pl-US                         |
| Nowa Kaledonia                            | NC                       | NCL                      | fr — FR/pl-US                         |
| Nowa Zelandia                              | NZ                       | NZL                      | EN-NZ/en-US                         |
| Nikaragua                                | NI                       | Karta sieciowa                      | ES — NI/en-US                         |
| Niger                                    | NE                       | NER                      | fr — FR/pl-US                         |
| Nigeria                                  | NG                       | NGA                      | ha-Latn-NG/pl-US                    |
| Niue                                     | NU                       | NIU                      | en-US                                 |
| Norfolk                           | OZNACZONA                       | NFK                      | en-US                                 |
| Mariany Północne                 | MP                       | MNP                      | en-US                                 |
| Norwegia                                   | NO                       | NOR                      | NB — NO/pl-US                         |
| Oman                                     | OM                       | OMN                      | AR-OM/pl-US                         |
| Pakistan                                 | PK                       | Pakiet                      | Twoje-PK/pl-US                         |
| Palau                                    | PW                       | PLW                      | en-US                                 |
| Autonomia Palestyńska                    | PS                       | PSE                      | ar-SA/pl-US                         |
| Panama                                   | PA                       | PAN                      | ES — PA/pl-US                         |
| Papua Nowa Gwinea                         | STRONY                       | PNG                      | en-US                                 |
| Paragwaj                                 | PY                       | PRY                      | ES — PR/pl                         |
| Peru                                     | PE                       | PER                      | ES — PE/pl-US                         |
| Filipiny                              | PH                       | PHL                      | EN-PH/pl-US                         |
| Wyspy Pitcairn                         | NC                       | PCN                      | en-US                                 |
| Polska                                   | PL                       | POL                      | pl-PL/pl-US                         |
| Portugalia                                 | PT                       | PRT                      | pt-PT/pl-US                         |
| Portoryko                              | PR                       | PRI                      | ES — PR/pl                         |
| Katar                                    | QA                       | QAT                      | AR-pytań i odpowiedzi na pl                         |
| Réunion                                  | RE                       | REU                      | fr — FR/pl-US                         |
| Rumunia                                  | RO                       | ROU                      | RO-RO/pl-US                         |
| Rosja                                   | RU                       | RUS                      | ru — RU/pl-US                         |
| Rwanda                                   | RW                       | RWA                      | RW-RW/pl-US                         |
| Saba                                     | XS                       | XSA                      | NL-NL/pl-US                         |
| Saint Kitts i Nevis                    | KN                       | KNA                      | pl-GB/pl-US                         |
| Saint Lucia                              | LC                       | DZIAŁU prawnego                      | en-US                                 |
| Saint-Martin                             | CZĘSTOTLIWOŚCI                       | WYNR                      | fr — FR/pl-US                         |
| Saint Pierre i Miquelon                | PM                       | SPM                      | fr — FR/pl-US                         |
| Saint Vincent i Grenadyny         | VC                       | VCT                      | en-US                                 |
| Saint-Barthélemy                         | BL                       | BLM                      | fr — FR/pl-US                         |
| Samoa                                    | WS                       | WSM                      | en-US                                 |
| San Marino                               | SPRZEDAŻY                       | SMR                      | IT/en-US                         |
| Wyspy Świętego Tomasza i Książęca                    | SKLEP                       | STP                      | pt-PT/pl-US                         |
| Arabia Saudyjska                             | SA                       | SAU                      | ar-SA/pl-US                         |
| Senegal                                  | SN                       | DAWCY                      | wo-SN/pl-US                         |
| Serbia                                   | RS                       | SRB                      | sr-latn-RS/SR-Cyrl-RS/en-US       |
| Seszele                               | SC                       | SYC                      | en-US                                 |
| Sierra Leone                             | SL                       | SLE                      | en-US                                 |
| Singapur                                | SG                       | SGP                      | EN-SG/zh-SG/pl-US                 |
| Sint Eustatius                           | HASŁA                       | XSE                      | NL-NL/pl-US                         |
| Sint Maarten                             | SX                       | SXM                      | en-US                                 |
| Słowacja                                 | SK                       | SVK                      | SK-SK/pl-US                         |
| Słowenia                                 | SI                       | SVN                      | SL-SI/pl-US                         |
| Wyspy Salomona                          | SB                       | USTAWIONYCH                      | en-US                                 |
| Somalia                                  | SO                       | SOM                      | ar-SA/pl-US                         |
| Republika Południowej Afryki                             | ZA                       | ZAF                      | pl-za/pl-US                         |
| Georgia Południowa i Sandwich Południowy | GS                       | MOIMI                      | en-US                                 |
| Sudan Południowy                              | SS                       | SSD                      | en-US                                 |
| Hiszpania                                    | ES                       | ESP                      | es-ES/CA-ES/UE-ES/GL-ES/pl-US |
| Sri Lanka                                | LK                       | LKA                      | si-LK/en-US                         |
| Święta Helena, Wyspa Wniebowstąpienia, Tristan da Cunha   | SH                       | SHN                      | en-US                                 |
| Surinam                                 | SR                       | SUR                      | nl-NL                                 |
| Svalbard                                 | SJ                       | SJM                      | NB — NO/pl-US                         |
| Szwecja                                   | SE                       | SWE                      | SV — SE/pl-US                         |
| Szwajcaria                              | CH                       | MIEŚĆ                      | de-CH/fr-CH/IT-CH/pl-US         |
| Tajwan                                   | TW                       | TWN                      | zh-TW/pl-US                         |
| Tadżykistan                               | TJ                       | TJK                      | TG-Cyrl-TJ/pl-US                    |
| Tanzania                                 | TZ                       | TZA                      | pl-GB/pl-US                         |
| Tajlandia                                 | TH                       | OKREŚLONA                      | th-TH/pl-US                         |
| Timor-Leste                              | TL                       | TLS                      | pt-PT/pl-US                         |
| Togo                                     | TG                       | TGO                      | fr — FR/pl-US                         |
| Tokelau                                  | TK                       | TKL                      | en-US                                 |
| Tonga                                    | TO                       | PRZEZNACZONE                      | en-US                                 |
| Trinidad i Tobago                      | TT                       | Aby                      | EN-TT/pl-US                         |
| Tunezja                                  | TN                       | TUN                      | AR-TN/pl-US                         |
| Turcja                                   | TR                       | TUR                      | TR-TR/pl-US                         |
| Turkmenistan                             | TM                       | TKM                      | TK-TM/pl-US                         |
| Wyspy Turks i Caicos                 | TC                       | ZAKUPU                      | en-US                                 |
| Tuvalu                                   | TV                       | TUV                      | en-US                                 |
| Uganda                                   | UG                       | UGA                      | pl-GB/pl-US                         |
| Ukraina                                  | UA                       | UKR                      | UK-UA/pl-US                         |
| Zjednoczone Emiraty Arabskie                     | AE                       | LEŻĄ                      | AR-AE/pl-US                         |
| Zjednoczone Królestwo                           | GB                       | GBR                      | pl-GB/pl-US                         |
| Odległe wyspy Stanów Zjednoczonych                    | UM                       | UMI                      | en-US                                 |
| Wyspy Dziewicze Stanów Zjednoczonych                      | VI                       | VIR                      | en-US                                 |
| Stany Zjednoczone                            | USA                       | USA                      | pl-US/es — US                         |
| Urugwaj                                  | UY                       | URY                      | ES — UY/pl-US                         |
| Uzbekistan                               | UZ                       | UZB                      | uz-Latn-UZ/pl-US                    |
| Vanuatu                                  | VU                       | VUT                      | en-US                                 |
| Watykan                             | VA                       | NIP                      | IT/en-US                         |
| Wenezuela                                | VE                       | Wet                      | ES — Zapisz/en-US                         |
| Wietnam                                  | VN                       | VNM                      | VI-VN/pl-US                         |
| Wallis i Futuna                        | WF                       | WLF                      | fr — FR/pl-US                         |
| Jemen                                    | YE                       | YEM                      | AR-YE/pl-US                         |
| Zambia                                   | ZM                       | ZMB                      | pl-GB/pl-US                         |
| Zimbabwe                                 | ZW                       | ZWE                      | EN-ZW/en-US                         |

