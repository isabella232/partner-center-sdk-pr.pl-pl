---
title: Języki obsługiwane przez Centrum partnerskie i ustawienia regionalne
description: Lista obsługiwanych przez iso2 i ISO3 ustawieniach regionalnych dla Partner Center.
ms.date: 12/03/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: cychua
ms.author: cychua
ms.openlocfilehash: b3a64cc6aa4b19199490dafcf15eedde12b1330a
ms.sourcegitcommit: b307fd75e305e0a88cfd1182cc01d2c9a108ce45
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/06/2021
ms.locfileid: "111547805"
---
# <a name="partner-center-supported-languages-and-locales"></a>Języki obsługiwane przez Centrum partnerskie i ustawienia regionalne

**Dotyczy:** Partner Center | Partner Center obsługiwana przez firmę 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government

Niektóre Partner Center API wymagają wartości wskazującej lokalne, kraj lub region. Na przykład nagłówek [REST Partner Center](headers.md) X-Locale wymaga często wartości w formacie "language-country" ("en-US" oznacza "Angielski — Stany Zjednoczone").

W zarządzanych interfejsach API usługi Partner Center klasa [CountryValidationRules/dotnet/api/microsoft.store.partnercenter.models.countryvalidationrules.countryvalidationrules) i klasa [OfferCategory.Locale/dotnet/api/microsoft.store.partnercenter.models.offers.offercategory.locale), [ServiceRequest.CountryCode/dotnet /api/microsoft.store.partnercenter.models.servicerequests.servicerequest.countrycode) lub [CustomerBillingProfile.Culture/dotnet/api/microsoft.store.partnercenter.models.customers.customerbillingprofile.culture) wymagają wartości ciągu wskazujących język lub kraj/region (w formie kodu języka ISO2 lub kodu kraju/regionu ISO3), ustawieniach regionalnych, lub kultury (identyfikator języka w połączeniu z kodem kraju/regionu).

W poniższej tabeli wymieniono kultury i kody krajów międzynarodowych organizacji standardowych (ISO), które są obsługiwane w Partner Center API.

| Kraj/region                           | ISO Alpha 2 Country Code | ISO Alpha 3 Country Code | Obsługiwane kultury                  |
|------------------------------------------|--------------------------|--------------------------|---------------------------------------|
| Afganistan                              | AF                       | Afg                      | ps-AF / en-US                         |
| Wyspy alandzkie                            | Ax                       | Ala                      | sv-SE / en-US                         |
| Albania                                  | AL                       | Alb                      | sq-AL / en-US                         |
| Algieria                                  | DZ                       | Dza                      | ar-EMA / en-US                         |
| Samoa Amerykańskie                           | AS                       | ASM                      | en-US                                 |
| Andora                                  | AD                       | AND                      | ca-ES / en-US                         |
| Angola                                   | AO                       | Temu                      | pt-PT / en-US                         |
| Anguilla                                 | Sztuczna inteligencja                       | Aia                      | en-US                                 |
| Antarktyda                               | Aq                       | Ata                      | en-US                                 |
| Antigua i Barbuda                      | AG                       | Atg                      | en-US                                 |
| Argentyna                                | AR                       | Arg                      | es-AR / en-US                         |
| Armenia                                  | AM                       | ARM                      | hy-AM / en-US                         |
| Aruba                                    | Awh                       | Abw                      | nl-NL / en-US                         |
| Australia                                | AU                       | Aus                      | en-AU / en-US                         |
| Austria                                  | AT                       | AUT                      | de-AT / en-US                         |
| Azerbejdżan                               | AZ                       | Aze                      | az-Latn-AZ / en-US                    |
| Bahamy                                  | BS                       | Bhs                      | en-GB / en-US                         |
| Bahrajn                                  | BH                       | Bhr                      | ar-BH / en-US                         |
| Bangladesz                               | BD                       | Bgd                      | bn-BD / en-US                         |
| Barbados                                 | BB                       | Brb                      | en-GB / en-US                         |
| Białoruś                                  | BY                       | BLR                      | be-BY / en-US                         |
| Belgia                                  | BE                       | Bel                      | fr-BE / nl-BE / en-US                 |
| Belize                                   | BZ                       | Blz                      | en-BZ / en-US                         |
| Benin                                    | BJ                       | Ben                      | fr-FR / en-US                         |
| Bermudy                                  | Bm                       | Bmu                      | en-GB / en-US                         |
| Bhutan                                   | BT                       | Btn                      | en-US                                 |
| Boliwia                                  | BO                       | Bol                      | es-BO / en-US                         |
| Bonaire                                  | Bq                       | Bes                      | nl-NL / en-US                         |
| Bośnia i Hercegowina                   | BA                       | Bih                      | bs-Latn-BA / en-US                    |
| Botswana                                 | BW                       | Bwa                      | en-GB / en-US                         |
| Wyspa Bouveta                            | Bv                       | Bvt                      | nb-NO / en-US                         |
| Brazylia                                   | BR                       | Biustonosz                      | pt-BR / en-US                         |
| Brytyjskie Terytorium Oceanu Indyjskiego           | WE/WY                       | IOT                      | en-US                                 |
| Brytyjskie Wyspy Dziewicze                   | VG                       | Vgb                      | en-US                                 |
| Brunei                                   | BN                       | Brn                      | ms-BN / en-US                         |
| Bułgaria                                 | BG                       | Bgr                      | bg-BG / en-US                         |
| Burkina Faso                             | BF                       | Bfa                      | fr-FR / en-US                         |
| Burundi                                  | BI                       | Bdi                      | fr-FR / en-US                         |
| Cabo Verde                               | CV                       | Cpv                      | pt-CV / en-US                         |
| Kambodża                                 | KH                       | Khm                      | km-KH / en-US                         |
| Kamerun                                 | CM                       | Cmr                      | fr-FR / en-US                         |
| Kanada                                   | CA                       | Cna                      | fr-CA / en-US                         |
| Kajmany                           | KY                       | CYM                      | en-GB / en-US                         |
| Republika Środkowoafrykańska                 | CF                       | Caf                      | fr-FR / en-US                         |
| Czad                                     | TD                       | Tcd                      | fr-FR / en-US                         |
| Chile                                    | CL                       | Chl                      | es-CL / en-US                         |
| Chiny                                    | CN                       | Chn                      | zh-CN / en-US                         |
| Wyspa Bożego Narodzenia                         | CX                       | CXR                      | en-US                                 |
| Wyspy Kokosowe (Keelinga)                  | CC                       | Cck                      | en-US                                 |
| Kolumbia                                 | CO                       | Płk                      | es-CO / en-US                         |
| Komory                                  | Km                       | Model COM                      | fr-FR / en-US                         |
| Kongo                                    | Cg                       | Cog                      | fr-FR / en-US                         |
| Kongo (DRK)                              | CD                       | COD                      | fr-FR / en-US                         |
| Wyspy Cooka                             | Ck                       | Cok                      | en-US                                 |
| Kostaryka                               | CR                       | Cri                      | es-CR / en-US                         |
| Côte d'Ivoire                            | CI                       | Civ                      | fr-FR / en-US                         |
| Chorwacja                                  | HR                       | Hrv                      | hr-HR / en-US                         |
| Curaçao                                  | Cw                       | CUW                      | nl-NL / en-US                         |
| Cypr                                   | CY                       | Cyp                      | el-GR / en-US                         |
| Czechy                                  | CZ                       | CZE                      | cs-CZ / en-US                         |
| Dania                                  | DK                       | Dnk                      | da-DK / en-US                         |
| Dżibuti                                 | Dj                       | Dji                      | fr-FR / en-US                         |
| Dominika                                 | DM                       | Narzędzie DMA                      | en-US                                 |
| Dominikana                       | DO                       | DOM                      | es-DO / en-US                         |
| Ekwador                                  | EC                       | Ecu                      | es-EC / en-US                         |
| Egipt                                    | EG                       | EGY                      | ar-EG / en-US                         |
| Salwador                              | SV                       | Slv                      | es-SV / en-US                         |
| Gwinea Równikowa                        | Gq                       | GNQ                      | es-ES / en-US                         |
| Erytrea                                  | ER                       | Eri                      | ar-SA / en-US                         |
| Estonia                                  | EE                       | Est                      | et-EE / en-US                         |
| eSwatini                                 | SZ                       | Swz                      | en-US                                 |
| Etiopia                                 | ET                       | Eth                      | am-ET / en-US                         |
| Falklandy                         | Fk                       | Flk                      | en-US                                 |
| Wyspy Owcze                            | Fo                       | Powrotem                      | fo-FO / en-US                         |
| Fidżi                                     | FJ                       | FJI                      | en-GB / en-US                         |
| Finlandia                                  | FI                       | FIN                      | fi-FI / sv-FI / en-US                 |
| Francja                                   | PW                       | FRA                      | fr-FR / en-US                         |
| Gujana Francuska                            | GF                       | GUF                      | fr-FR / en-US                         |
| Polinezja Francuska                         | PF                       | PYF                      | fr-FR / en-US                         |
| Francuskie Terytoria Południowe i Antarktyczne              | Tf                       | Atf                      | fr-FR / en-US                         |
| Gabon                                    | Ogólna dostępność                       | Gab                      | fr-FR / en-US                         |
| Gambia                                   | GM                       | Gmb                      | en-US                                 |
| Gruzja                                  | GE                       | Geo                      | ka-GE / en-US                         |
| Niemcy                                  | DE                       | DEU                      | de-DE / en-US                         |
| Ghana                                    | GH                       | Gha                      | en-GB / en-US                         |
| Gibraltar                                | Gi                       | Gib                      | en-US                                 |
| Grecja                                   | GR                       | GRC                      | el-GR / en-US                         |
| Grenlandia                                | Gl                       | Grl                      | da-DK /en-US                         |
| Grenada                                  | Gd                       | Grd                      | en-US                                 |
| Gwadelupa                               | GP                       | Glp                      | fr-FR / en-US                         |
| Guam                                     | GU                       | Dziąseł                      | en-US                                 |
| Gwatemala                                | GT                       | Gtm                      | es-GT / en-US                         |
| Guernsey                                 | Gg                       | GGY                      | en-US                                 |
| Gwinea                                   | GN                       | Gin                      | fr-FR / en-US                         |
| Gwinea Bissau                            | Gw                       | Gnb                      | pt-PT / en-US                         |
| Gujana                                   | GY                       | Facet                      | en-US                                 |
| Haiti                                    | HT                       | Hti                      | fr-FR / en-US                         |
| Wyspy Heard i McDonalda        | Hm                       | Hmd                      | en-US                                 |
| Honduras                                 | HN                       | Hnd                      | es-HN / en-US                         |
| SRA Hongkong                            | HK                       | Hkg                      | zh-HK /en-US                         |
| Węgry                                  | HU                       | HUN                      | hu-HU / en-US                         |
| Islandia                                  | IS                       | Isl                      | is-IS / en-US                         |
| Indie                                    | IN                       | IND                      | en-IN / hi-IN / en-US                 |
| Indonezja                                | ID (Identyfikator)                       | Idn                      | id-ID / en-US                         |
| Irak                                     | IQ                       | Irq                      | ar-IQ / en-US                         |
| Irlandia                                  | IE                       | Irl                      | en-IE / en-US                         |
| Wyspa Man                              | WIADOMOŚĆ BŁYSKAWICZNA                       | Imn                      | en-US                                 |
| Izrael                                   | IL                       | ISR                      | he-IL / en-US                         |
| Włochy                                    | IT                       | ITA                      | it-IT/en-US                         |
| Jamajka                                  | JM                       | Jam                      | en-JM / en-US                         |
| Jan Mayen                                | Xj                       | XJA                      | nb-NO / en-US                         |
| Japonia                                    | JP                       | JPN                      | ja-JP / en-US                         |
| Jersey                                   | JE                       | Jey                      | en-US                                 |
| Jordania                                   | JO                       | Jor                      | ar-JO / en-US                         |
| Kazachstan                               | KZ                       | Kaz                      | kk-KZ / en-US                         |
| Kenia                                    | KE                       | Ken                      | sw-KE / en-US                         |
| Kiribati                                 | KI                       | Kir                      | en-US                                 |
| Korea                                    | KR                       | KOR                      | ko-KR / en-US                         |
| Kosowo                                   | Xk                       | Xks                      | en-US                                 |
| Kuwejt                                   | KW                       | KWT                      | ar-KW / en-US                         |
| Kirgistan                               | KG                       | KGZ                      | ky-KG / en-US                         |
| Laos                                     | LA                       | Lao                      | lo-LA / en-US                         |
| Łotwa                                   | LV                       | Lva                      | lv-LV / en-US                         |
| Liban                                  | LB                       | LbN                      | ar-LB / en-US                         |
| Lesotho                                  | LS                       | Lso                      | en-US                                 |
| Liberia                                  | LR                       | Lbr                      | en-US                                 |
| Libia                                    | LY                       | LbY                      | ar-LY / en-US                         |
| Liechtenstein                            | LI                       | Kłamstwo                      | de-LI / en-US                         |
| Litwa                                | LT                       | Ltu                      | lt-LT / en-US                         |
| Luksemburg                               | LU                       | Lux                      | de-LU / fr-LU / en-US                 |
| SRA Makau                                | MO                       | Komputerze mac                      | zh-MO / en-US                         |
| Republika Północna i Północna                          | MK                       | Mkd                      | mk-MK / en-US                         |
| Madagaskar                               | MG                       | Mcr                      | fr-FR / en-US                         |
| Malawi                                   | MW                       | Mwi                      | en-US                                 |
| Malezja                                 | MY                       | Mys                      | en-MY / en-US                         |
| Malediwy                                 | MV                       | Mdv                      | dv-MV / en-US                         |
| Mali                                     | ML                       | Mli                      | fr-FR / en-US                         |
| Malta                                    | MT                       | Mlt                      | mt-MT / en-US                         |
| Wyspy Marshalla                         | MH                       | Mhl                      | en-US                                 |
| Martynika                               | MQ                       | MTQ                      | fr-FR / en-US                         |
| Mauretania                               | MR                       | Mrt                      | ar-SA / en-US                         |
| Mauritius                                | Mu (MU)                       | Mus                      | en-GB / en-US                         |
| Wyspa Majotta                                  | YT                       | Myt                      | fr-FR / en-US                         |
| Meksyk                                   | MX                       | Mex                      | es-MX / en-US                         |
| Mikronezja                               | FM                       | Fsm                      | en-US                                 |
| Mołdawia                                  | MD                       | Mda                      | ro-RO / en-US                         |
| Monako                                   | MC                       | Mco                      | fr-MC / en-US                         |
| Mongolia                                 | MN                       | Mng                      | mn-MN / en-US                         |
| Czarnogóra                               | ME                       | Mne                      | sr-Latn-ME / en-US                    |
| Montserrat                               | MS                       | MSR                      | en-US                                 |
| Maroko                                  | MA                       | MAR                      | ar-MA / en-US                         |
| Mozambik                               | MZ                       | Moz                      | pt-PT                                 |
| Myanmar                                  | MM                       | Mmr                      | en-US                                 |
| Namibia                                  | NA                       | NAM (NAZWA)                      | en-GB / en-US                         |
| Nauru                                    | NR                       | Nru                      | en-US                                 |
| Nepal                                    | NP                       | Npl                      | ne-NP / en-US                         |
| Antyle Holenderskie                     | z o.o.                       | Ant                      | en-US                                 |
| Holandia,                         | NL                       | NLD                      | nl-NL / en-US                         |
| Nowa Kaledonia                            | NC                       | NCL                      | fr-FR / en-US                         |
| Nowa Zelandia                              | NZ                       | Nzl                      | en-NZ / en-US                         |
| Nikaragua                                | NI                       | Karta sieciowa                      | es-NI / en-US                         |
| Niger                                    | NE                       | Ner                      | fr-FR / en-US                         |
| Nigeria                                  | NG                       | Nga                      | ha-Latn-NG / en-US                    |
| Niue                                     | NU                       | Niu                      | en-US                                 |
| Norfolk                           | Nf                       | NFK                      | en-US                                 |
| Mariany Północne                 | MP                       | MNP                      | en-US                                 |
| Norwegia                                   | NO                       | NOR                      | nb-NO / en-US                         |
| Oman                                     | OM                       | Omn                      | ar-OM / en-US                         |
| Pakistan                                 | PK                       | Pak                      | Your-PK / en-US                         |
| Palau                                    | PW                       | Plw                      | en-US                                 |
| Autonomia Palestyńska                    | PS                       | Pse                      | ar-SA / en-US                         |
| Panama                                   | PA                       | PAN                      | es-PA / en-US                         |
| Papua Nowa Gwinea                         | Str                       | PNG                      | en-US                                 |
| Paragwaj                                 | PY                       | Podważyć                      | es-PY /en-US                         |
| Peru                                     | PE                       | PER                      | es-PE / en-US                         |
| Filipiny                              | PH                       | Phl                      | en-PH / en-US                         |
| Wyspy Pitcairn                         | Pn                       | Pcn                      | en-US                                 |
| Polska                                   | PL                       | Pol                      | pl-PL / en-US                         |
| Portugalia                                 | PT                       | Prt                      | pt-PT / en-US                         |
| Portoryko                              | PR                       | Pri                      | es-PR / en-US                         |
| Katar                                    | QA                       | QAT                      | ar-QA / en-US                         |
| Réunion                                  | RE                       | Reu                      | fr-FR / en-US                         |
| Rumunia                                  | RO                       | Rou                      | ro-RO / en-US                         |
| Rosja                                   | RU                       | RUS                      | ru-RU / en-US                         |
| Rwanda                                   | RW                       | Rwa                      | rw-RW / en-US                         |
| Saba                                     | Xs                       | Xsa                      | nl-NL / en-US                         |
| Saint Kitts i Nevis                    | KN                       | Kna                      | en-GB / en-US                         |
| Saint Lucia                              | Lc                       | Lca                      | en-US                                 |
| Saint-Martin                             | Mf                       | Maf                      | fr-FR / en-US                         |
| Saint Pierre i Miquelon                | PM                       | Spm                      | fr-FR / en-US                         |
| Saint Vincent i Grenadyny         | VC                       | Vct                      | en-US                                 |
| Saint-Barthélemy                         | BL                       | Blm                      | fr-FR / en-US                         |
| Samoa                                    | WS                       | Wsm                      | en-US                                 |
| San Marino                               | Sm                       | Smr                      | it-IT/en-US                         |
| São Tomé i Prüncipe                    | SKLEP                       | Stp                      | pt-PT / en-US                         |
| Arabia Saudyjska                             | SA                       | Sau                      | ar-SA / en-US                         |
| Senegal                                  | SN                       | Senator                      | wo-SN / en-US                         |
| Serbia                                   | RS                       | Srb                      | sr-Latn-RS / sr-Cyrl-RS / en-US       |
| Seszele                               | SC                       | Syc                      | en-US                                 |
| Sierra Leone                             | SL                       | Sle                      | en-US                                 |
| Singapur                                | SG                       | Sgp                      | en-SG / zh-SG / en-US                 |
| Sint Eustatius                           | Xe                       | XSE                      | nl-NL / en-US                         |
| Sint Maarten                             | Sx                       | Sxm                      | en-US                                 |
| Słowacja                                 | SK                       | Svk                      | sk-SK / en-US                         |
| Słowenia                                 | SI                       | Svn                      | sl-SI / en-US                         |
| Wyspy Salomona                          | Sb                       | Slb                      | en-US                                 |
| Somalia                                  | SO                       | Som                      | ar-SA / en-US                         |
| Republika Południowej Afryki                             | ZA                       | Zaf                      | en-ZA / en-US                         |
| Georgia Południowa i Sandwich Południowy | Gs                       | Sgs                      | en-US                                 |
| Sudan Południowy                              | SS                       | SSD                      | en-US                                 |
| Hiszpania                                    | ES                       | Esp                      | es-ES / ca-ES / eu-ES / gl-ES / en-US |
| Sri Lanka                                | LK                       | ZAJ.                      | si-LK / en-US                         |
| StRowa, Ascension, Tristan da Cunha   | SH                       | Shn                      | en-US                                 |
| Surinam                                 | SR                       | Sur                      | nl-NL                                 |
| Svalbard                                 | Sj                       | SJM                      | nb-NO / en-US                         |
| Szwecja                                   | SE                       | ZAIMKI                      | sv-SE / en-US                         |
| Szwajcaria                              | CH                       | Che                      | de-CH / fr-CH / it-CH / en-US         |
| Tajwan                                   | TW                       | Twn                      | zh-TW / en-US                         |
| Tadżykistan                               | Tj.                       | TjK                      | tg-Cyrl-TJ / en-US                    |
| Tanzania                                 | TZ                       | TZA                      | en-GB / en-US                         |
| Tajlandia                                 | TH                       | Tha                      | th-TH / en-US                         |
| Timor-Leste                              | TL                       | TLS                      | pt-PT / en-US                         |
| Togo                                     | TG                       | Tgo                      | fr-FR / en-US                         |
| Tokelau                                  | Tk                       | Tkl                      | en-US                                 |
| Tonga                                    | TO                       | TON                      | en-US                                 |
| Trinidad i Tobago                      | TT                       | Tto                      | en-TT / en-US                         |
| Tunezja                                  | TN                       | Tun                      | ar-TN / en-US                         |
| Turcja                                   | TR                       | Tur                      | tr-TR / en-US                         |
| Turkmenistan                             | TM                       | Tkm                      | tk-TM / en-US                         |
| Wyspy Turks i Caicos                 | TC                       | Tca                      | en-US                                 |
| Tuvalu                                   | TV                       | TUV                      | en-US                                 |
| Uganda                                   | UG                       | UGA                      | en-GB / en-US                         |
| Ukraina                                  | UA                       | Ukr                      | uk-UA / en-US                         |
| Zjednoczone Emiraty Arabskie                     | AE                       | Są                      | ar-AE / en-US                         |
| Zjednoczone Królestwo                           | GB                       | Gbr                      | en-GB / en-US                         |
| Stany Zjednoczone Odlying Islands                    | UM                       | Umi                      | en-US                                 |
| Wyspy Dziewicze Stanów Zjednoczonych                      | VI                       | Vir                      | en-US                                 |
| Stany Zjednoczone                            | USA                       | USA                      | en-US / es-US                         |
| Urugwaj                                  | UY                       | Ury                      | es-UY / en-US                         |
| Uzbekistan                               | UZ                       | UZB                      | uz-Latn-UZ / en-US                    |
| Vanuatu                                  | Vu                       | VUT                      | en-US                                 |
| Watykan                             | VA                       | Podatku vat                      | it-IT /en-US                         |
| Wenezuela                                | VE                       | Ven                      | es-VE / en-US                         |
| Wietnam                                  | VN                       | Vnm                      | vi-VN / en-US                         |
| Wallis i Ichuna                        | WF                       | Wlf                      | fr-FR / en-US                         |
| Jemen                                    | Ye                       | YEM                      | ar-YE / en-US                         |
| Zambia                                   | ZM                       | Zmb                      | en-GB / en-US                         |
| Zimbabwe                                 | ZW                       | ZWE                      | en-ZW / en-US                         |

