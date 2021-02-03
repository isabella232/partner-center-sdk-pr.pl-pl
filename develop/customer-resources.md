---
title: Zasoby klienta
description: Zasoby klienta reprezentujące klienta lub odsprzedawcy.
ms.date: 11/13/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: dineshvu
ms.author: dineshvu
ms.openlocfilehash: fbd72ab5710876ba303fd1e30e6e552ecf89c5cd
ms.sourcegitcommit: 741cfa8585901de207c2e5da5eeebe26db0b0ad1
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/18/2020
ms.locfileid: "97768573"
---
# <a name="customer-resources"></a>Zasoby klienta

**Dotyczy:**

- Centrum partnerskie
- Centrum partnerskie obsługiwane przez firmę 21Vianet
- Centrum partnerskie dla Microsoft Cloud Niemcy
- Centrum partnerskie Microsoft Cloud for US Government

## <a name="customer"></a>Klient

Zasób **klienta** reprezentuje klienta lub odsprzedawcy. W większości przypadków zasób klienta może być dowolną osobą, pracownikiem lub organizacją, która chce przeprowadzić działalność z odsprzedawcami firmy Microsoft i Microsoft. Klienci mają również profil firmy i profil rozliczeń.

>[!NOTE]
>Zasób **klienta** ma limit stawki 500 żądań na minutę na identyfikator dzierżawy.

| Właściwość              | Typ                                                             | Opis                                                                                                                                  |
|-----------------------|------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------|
| identyfikator                    | ciąg                                                           | Identyfikator klienta.                                                                                                                             |
| commerceId            | ciąg                                                           | Identyfikator handlowy.                                                                                                                             |
| companyProfile        | [CustomerCompanyProfile](#customercompanyprofile)                | Dodatkowe informacje na temat firmy lub organizacji.                                                                                    |
| billingProfile        | [CustomerBillingProfile](#customerbillingprofile)                | Dodatkowe informacje używane do rozliczania.                                                                                                     |
| relationshipToPartner | ciąg                                                           | Definiuje program licencjonowania, którego partner używa dla tego klienta: "none", "Odsprzedawca", "Advisor", "zespalanie" lub " \_ Pomoc techniczna firmy Microsoft". |
| allowDelegatedAccess  | boolean                                                          | Czy partnerowi udzielono uprawnień administratora delegowanego przez tego klienta. Ta właściwość jest dostępna tylko w przypadku otrzymania klienta według identyfikatora, a nie według listy.                                                         |
| userCredentials       | [UserCredentials](user-resources.md#usercredentials) | Poświadczenia użytkownika.                                                                                                                        |
| customDomains         | tablica ciągów                                                 | Lista domen niestandardowych klienta.                                                                                                        |
| associatedPartnerId   | ciąg                                                           | Pośredni odsprzedawcy skojarzony z tym kontem klienta. Tę wartość można ustawić tylko przez pośrednich partnerów CSP.                              |
| linki                 | [ResourceLinks](utility-resources.md#resourcelinks)             | Linki do zasobów zawarte w profilu.                                                                                             |
| atrybuty            | [ResourceAttributes](utility-resources.md#resourceattributes)   | Atrybuty metadanych odpowiadające profilowi.                                                                                        |

## <a name="customercompanyprofile"></a>CustomerCompanyProfile

Zasób **CustomerCompanyProfile** to dodatkowe informacje o firmie lub organizacji.

| Właściwość    | Typ                                                           | Opis                                                                       |
|-------------|----------------------------------------------------------------|-----------------------------------------------------------------------------------|
| tenantId    | ciąg                                                         | Identyfikator dzierżawy klienta usługi Azure AD. Jest to również nazywane MicrosoftID. |
| domena      | ciąg                                                         | Nazwa klienta, na przykład contoso.onmicrosoft.com.                             |
| companyName | ciąg                                                         | Nazwa firmy lub organizacji.                                          |
| linki       | [ResourceLinks](utility-resources.md#resourcelinks)           | Linki do zasobów zawarte w profilu.                                  |
| atrybuty  | [ResourceAttributes](utility-resources.md#resourceattributes) | Atrybuty metadanych odpowiadające profilowi.                             |

| organizationRegistrationNumber | Ciąg | Numer identyfikacyjny organizacji klienta (określany również jako numer INN w niektórych krajach). Wymagane tylko dla firmy lub organizacji klienta w następujących krajach. Armenia (AM), Azerbejdżan (AZ), Białoruś (przez), Węgry (HU), Kazachstan (KZ), Kirgistan (KG), Mołdawia (MD), Rosja (RU), Tadżykistan (TJ), Uzbekistan (UZ), Ukraina (UA). W przypadku firmy/organizacji klienta znajdującej się w innych krajach nie należy określać jej. |


## <a name="customerbillingprofile"></a>CustomerBillingProfile

Zasób **CustomerBillingProfile** to dodatkowe informacje używane do naliczania opłat dla klienta.

| Właściwość       | Typ                                                           | Opis                                                                                                                                            |
|----------------|----------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
| identyfikator             | ciąg                                                         | Identyfikator profilu.                                                                                                                                |
| firstName      | ciąg                                                         | Imię kontaktu rozliczeń od firmy klienta. Jest to osoba, do której będą kierowane faktury i inne komunikaty o rozliczeniach. |
| lastName       | ciąg                                                         | Nazwisko kontaktu rozliczeń.                                                                                                                  |
| poczta e-mail          | ciąg                                                         | Adres e-mail kontaktu z rozliczeniami                                                                                                                    |
| kultura        | ciąg                                                         | Ich preferowana kultura do komunikacji i waluty, na przykład "en-us".                                                                               |
| language       | ciąg                                                         | Preferowany język do komunikacji.                                                                                                            |
| companyName    | ciąg                                                         | Nazwa firmy lub organizacji.                                                                                                               |
| defaultAddress | [Adres](utility-resources.md#address)                       | Adres, na który są wysyłane rachunki, gdzie działa kontakt rozliczania.                                                                                   |
| linki          | [ResourceLinks](utility-resources.md#resourcelinks)           | Linki do zasobów zawarte w profilu.                                                                                                       |
| atrybuty     | [ResourceAttributes](utility-resources.md#resourceattributes) | Atrybuty metadanych odpowiadające profilowi.                                                                                                  |

## <a name="customerrelationshiprequest"></a>CustomerRelationshipRequest

Zasób **CustomerRelationshipRequest** zawiera adres URL używany przez klienta do nawiązania relacji odsprzedawcy z partnerem.

| Właściwość   | Typ                                                           | Opis                                                              |
|------------|----------------------------------------------------------------|--------------------------------------------------------------------------|
| url        | ciąg                                                         | Adres URL używany przez klienta do nawiązania relacji z partnerem. |
| atrybuty | [ResourceAttributes](utility-resources.md#resourceattributes) | Atrybuty metadanych odpowiadające żądaniu relacji.       |