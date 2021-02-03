---
title: Zasoby informacji o kraju
description: Dowiedz się więcej o korzystaniu z interfejsów API Centrum partnerskiego z zasobami informacji o kraju i metadanymi opisowymi związanymi z określonym krajem lub regionem.
ms.date: 05/23/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: ba0974cf736ff86038f8abf9c77d6a648984d1df
ms.sourcegitcommit: 4c253abb24140a6e00b0aea8e79a08823ea5a623
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/07/2020
ms.locfileid: "97770140"
---
# <a name="country-information-resources-available-from-partner-center-apis"></a>Zasoby informacji o kraju dostępne z interfejsów API Centrum partnerskiego

**Dotyczy:**

- Centrum partnerskie
- Centrum partnerskie obsługiwane przez firmę 21Vianet
- Centrum partnerskie dla Microsoft Cloud Niemcy
- Centrum partnerskie Microsoft Cloud for US Government

Następujące zasoby są opisowymi metadanymi dla kraju/regionu.

## <a name="countryinformation"></a>CountryInformation

| Właściwość                      | Typ               | Opis                                                                                        |
|-------------------------------|--------------------|----------------------------------------------------------------------------------------------------|
| ExtensionData —                 | ciąg             | Dane rozszerzenia.                                                                                |
| Iso2Code                      | ciąg             | Kod ISO-2.                                                                                     |
| Iso3Code                      | ciąg             | Kod ISO-3.                                                                                     |
| DefaultCulture                | ciąg             | Domyślna kultura.                                                                               |
| IsStateRequired               | boolean            | Wskazuje, czy Województwo jest wymagane, czy nie.                                             |
| SupportedStatesList           | tablica ciągów   | Jeśli jest wymagana wartość State/Województwo, zwraca pełną listę dla tego kraju/regionu.                    |
| SupportedLanguagesList        | tablica ciągów   | Lista obsługiwanych języków.                                                                     |
| SupportedCulturesList         | tablica ciągów   | Lista obsługiwanych kultur.                                                                      |
| IsPostalCodeRequired          | boolean            | Wskazuje, czy kod pocztowy lub kod pocztowy są wymagane.                                    |
| PostalCodeRegex               | ciąg             | Wyrażenie regularne, które definiuje kod pocztowy.                                          |
| IsCityRequired                | boolean            | Wskazuje, czy miasto jest wymagane, czy nie.                                                       |
| IsVatIdSupported              | boolean            | Wskazuje, czy wymagany jest identyfikator płatnika podatku VAT.                                                     |
| TaxIdFormat                   | ciąg             | Format identyfikatora podatku.                                                                                 |
| TaxIdSample                   | ciąg             | Przykład identyfikatora podatkowego.                                                                                 |
| VatIdRegex                    | ciąg             | Wyrażenie regularne identyfikatora podatku.                                                                     |
| PhoneNumberRegex              | ciąg             | Wyrażenie regularne numeru telefonu.                                                               |
| IsRegistrationNumberSupported | boolean            | Wskazuje, czy numer rejestracji jest obsługiwany.                                       |
| IsTaxIdSupported              | boolean            | Wskazuje, czy identyfikator podatkowy jest obsługiwany. Jest to inne niż IsVatIdSupported. |
| ResellerAgreementRegion       | ciąg             | Region umowy odsprzedawcy.                                                                     |
| GeographicRegion              | ciąg             | Region geograficzny.                                                                             |
| CountryCallingCodesList       | tablica ciągów   | Kody wywoływania obsługiwane w kraju/regionie.                                                 |
| Atrybuty                    | ResourceAttributes | Atrybuty metadanych odpowiadające zasobowi CountryInformation.                          |

## <a name="countryvalidationrules"></a>CountryValidationRules

Opisuje reguły formatowania adresów dla kraju/regionu.

| Właściwość                | Typ               | Opis                                                                                        |
|-------------------------|--------------------|----------------------------------------------------------------------------------------------------|
| Iso2Code                | ciąg             | Kod ISO-2.                                                                                     |
| DefaultCulture          | ciąg             | Domyślna kultura.                                                                               |
| IsStateRequired         | boolean            | Wskazuje, czy Województwo jest wymagane, czy nie.                                             |
| SupportedStatesList     | tablica ciągów   | Jeśli jest wymagana wartość State/Województwo, zwraca pełną listę dla tego kraju/regionu.                    |
| SupportedLanguagesList  | tablica ciągów   | Lista obsługiwanych języków.                                                                     |
| SupportedCulturesList   | tablica ciągów   | Lista obsługiwanych kultur.                                                                      |
| IsPostalCodeRequired    | boolean            | Wskazuje, czy kod pocztowy lub kod pocztowy są wymagane.                                    |
| PostalCodeRegex         | ciąg             | Wyrażenie regularne, które definiuje kod pocztowy.                                          |
| IsCityRequired          | boolean            | Wskazuje, czy miasto jest wymagane, czy nie.                                                       |
| IsVatIdSupported        | boolean            | Wskazuje, czy wymagany jest identyfikator płatnika podatku VAT.                                                     |
| TaxIdFormat             | ciąg             | Format identyfikatora podatku.                                                                                 |
| TaxIdSample             | ciąg             | Przykład identyfikatora podatkowego.                                                                                 |
| VatIdRegex              | ciąg             | Wyrażenie regularne identyfikatora podatku.                                                                     |
| PhoneNumberRegex        | ciąg             | Wyrażenie regularne numeru telefonu.                                                               |
| IsTaxIdSupported        | boolean            | Wskazuje, czy identyfikator podatkowy jest obsługiwany. Ta właściwość jest różna od IsVatIdSupported. |
| IsTaxIdOptional         | boolean            | Wskazuje, czy identyfikator podatkowy jest opcjonalny, czy nie.                                                     |
| CountryCallingCodesList | tablica ciągów   | Kody wywoływania obsługiwane w kraju/regionie.                                                 |
| Atrybuty              | ResourceAttributes | Atrybuty metadanych odpowiadające zasobowi CountryInformation.                          |
