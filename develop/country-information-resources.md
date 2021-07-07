---
title: Zasoby informacji o kraju
description: Dowiedz się więcej o Partner Center API z zasobami informacji o kraju i metadanymi opisowymi powiązanymi z określonym kraju lub regionem.
ms.date: 05/23/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: caf56282d21df35ae9e179a98a37317f864117a3
ms.sourcegitcommit: ad8082bee01fb1f57da423b417ca1ca9c0df8e45
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/10/2021
ms.locfileid: "111973829"
---
# <a name="country-information-resources-available-from-partner-center-apis"></a>Zasoby informacji o kraju dostępne z Partner Center API

**Dotyczy:** Partner Center | Partner Center obsługiwana przez firmę 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government

Następujące zasoby to metadane opisowe dla kraju/regionu.

## <a name="countryinformation"></a>CountryInformation (Informacje o kraju)

| Właściwość                      | Typ               | Opis                                                                                        |
|-------------------------------|--------------------|----------------------------------------------------------------------------------------------------|
| Extensiondata                 | ciąg             | Dane rozszerzenia.                                                                                |
| Iso2Code                      | ciąg             | Kod ISO-2.                                                                                     |
| Iso3Code                      | ciąg             | Kod ISO-3.                                                                                     |
| DefaultCulture                | ciąg             | Kultura domyślna.                                                                               |
| IsStateRequired               | boolean            | Wskazuje, czy stan/województwo jest wymagane.                                             |
| SupportedStatesList           | tablica ciągów   | Jeśli stan/województwo jest wymagane, zwraca pełną listę dla tego kraju/regionu.                    |
| SupportedLanguagesList        | tablica ciągów   | Lista obsługiwanych języków.                                                                     |
| SupportedCulturesList         | tablica ciągów   | Lista obsługiwanych kultur.                                                                      |
| IsPostalCodeRequired          | boolean            | Wskazuje, czy kod pocztowy jest wymagany, czy nie.                                    |
| PostalCodeRegex               | ciąg             | Wyrażenie regularne definiujące kod pocztowy.                                          |
| IsCityRequired                | boolean            | Wskazuje, czy miasto jest wymagane.                                                       |
| IsVatIdSupported              | boolean            | Wskazuje, czy identyfikator VAT jest wymagany, czy nie.                                                     |
| TaxIdFormat                   | ciąg             | Format identyfikatora podatkowego.                                                                                 |
| TaxIdSample                   | ciąg             | Przykładowy identyfikator podatkowy.                                                                                 |
| VatIdRegex                    | ciąg             | Wyrażenie regularne identyfikatora podatkowego.                                                                     |
| PhoneNumberRegex              | ciąg             | Wyrażenie regularne numeru telefonu.                                                               |
| IsRegistrationNumberSupported | boolean            | Wskazuje, czy numer rejestracji jest obsługiwany.                                       |
| IsTaxIdSupported              | boolean            | Wskazuje, czy identyfikator podatkowy jest obsługiwany. Różni się to od isVatIdSupported. |
| ResellerAgreementRegion (Region odsprzedawcy)       | ciąg             | Region umowy odsprzedawcy.                                                                     |
| GeographicRegion (Region geograficzny)              | ciąg             | Region geograficzny.                                                                             |
| CountryCallingCodesList       | tablica ciągów   | Kody połączeń obsługiwane w kraju/regionie.                                                 |
| Atrybuty                    | ResourceAttributes | Atrybuty metadanych odpowiadające zasobowi CountryInformation.                          |

## <a name="countryvalidationrules"></a>CountryValidationRules

Opisuje reguły formatowania adresów dla kraju/regionu.

| Właściwość                | Typ               | Opis                                                                                        |
|-------------------------|--------------------|----------------------------------------------------------------------------------------------------|
| Iso2Code                | ciąg             | Kod ISO-2.                                                                                     |
| DefaultCulture          | ciąg             | Kultura domyślna.                                                                               |
| IsStateRequired         | boolean            | Wskazuje, czy stan/województwo jest wymagane.                                             |
| SupportedStatesList     | tablica ciągów   | Jeśli stan/województwo jest wymagane, zwraca pełną listę dla tego kraju/regionu.                    |
| SupportedLanguagesList  | tablica ciągów   | Lista obsługiwanych języków.                                                                     |
| SupportedCulturesList   | tablica ciągów   | Lista obsługiwanych kultur.                                                                      |
| IsPostalCodeRequired    | boolean            | Wskazuje, czy kod pocztowy jest wymagany, czy nie.                                    |
| PostalCodeRegex         | ciąg             | Wyrażenie regularne definiujące kod pocztowy.                                          |
| IsCityRequired          | boolean            | Wskazuje, czy miasto jest wymagane.                                                       |
| IsVatIdSupported        | boolean            | Wskazuje, czy identyfikator VAT jest wymagany, czy nie.                                                     |
| TaxIdFormat             | ciąg             | Format identyfikatora podatkowego.                                                                                 |
| TaxIdSample             | ciąg             | Przykładowy identyfikator podatkowy.                                                                                 |
| VatIdRegex              | ciąg             | Wyrażenie regularne identyfikatora podatkowego.                                                                     |
| PhoneNumberRegex        | ciąg             | Wyrażenie regularne numeru telefonu.                                                               |
| IsTaxIdSupported        | boolean            | Wskazuje, czy identyfikator podatkowy jest obsługiwany. Ta właściwość jest inna niż IsVatIdSupported. |
| IsTaxIdOptional         | boolean            | Wskazuje, czy identyfikator podatkowy jest opcjonalny.                                                     |
| CountryCallingCodesList | tablica ciągów   | Kody połączeń obsługiwane w kraju/regionie.                                                 |
| Atrybuty              | ResourceAttributes | Atrybuty metadanych odpowiadające zasobowi CountryInformation.                          |
