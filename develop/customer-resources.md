---
title: Zasoby klienta
description: Zasoby klienta, które reprezentują klienta lub odsprzedawcę.
ms.date: 03/30/2021
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: dineshvu
ms.author: dineshvu
ms.openlocfilehash: 10798ae0bfae8c1a4e38777096861427992b8aee3799ee2dd9154c6f0e0c0799
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/06/2021
ms.locfileid: "115995173"
---
# <a name="customer-resources"></a>Zasoby klienta

**Dotyczy:** Partner Center | Partner Center obsługiwana przez firmę 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government

## <a name="customer"></a>Customer

Zasób **Customer** reprezentuje klienta lub odsprzedawcę. W większości przypadków zasób klienta może być dowolną osobą, pracownikiem lub organizacją, która chce korzystać z usług firmy Microsoft i odsprzedawców firmy Microsoft. Klienci mają również profil firmy i profil rozliczeniowy.

>[!NOTE]
>**Zasób** Klient ma limit szybkości 500 żądań na minutę na identyfikator dzierżawy.

| Właściwość              | Typ                                                             | Opis                                                                                                                                  |
|-----------------------|------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------|
| identyfikator                    | ciąg                                                           | Identyfikator klienta.                                                                                                                             |
| commerceId            | ciąg                                                           | Identyfikator handlowy.                                                                                                                             |
| companyProfile        | [CustomerCompanyProfile](#customercompanyprofile)                | Dodatkowe informacje o firmie lub organizacji.                                                                                    |
| billingProfile        | [CustomerBillingProfile](#customerbillingprofile)                | Dodatkowe informacje używane do rozliczeń.                                                                                                     |
| relationshipToPartner | ciąg                                                           | Definiuje program licencjonowania używany przez partnera dla tego klienta: "brak", "odsprzedawca", "doradca", "syndykacja" lub "pomoc techniczna \_ firmy Microsoft". |
| allowDelegatedAccess  | boolean                                                          | Wskazuje, czy partnerowi udzielono delegowanych uprawnień administratora przez tego klienta. Ta właściwość jest dostępna tylko podczas uzyskiwania klienta według identyfikatora, a nie według listy.                                                         |
| userCredentials       | [UserCredentials](user-resources.md#usercredentials) | Poświadczenia użytkownika.                                                                                                                        |
| customDomains         | tablica ciągów                                                 | Lista domen niestandardowych klienta.                                                                                                        |
| associatedPartnerId   | ciąg                                                           | Odsprzedawca pośredni skojarzony z tym kontem klienta. Tę wartość można ustawić tylko przez pośrednich partnerów CSP.                              |
| Linki                 | [ResourceLinks](utility-resources.md#resourcelinks)             | Linki zasobów zawarte w profilu.                                                                                             |
| atrybuty            | [ResourceAttributes](utility-resources.md#resourceattributes)   | Atrybuty metadanych odpowiadające profilowi.                                                                                        |

## <a name="customercompanyprofile"></a>CustomerCompanyProfile

Zasób **CustomerCompanyProfile** zawiera dodatkowe informacje o firmie lub organizacji.

| Właściwość    | Typ                                                           | Opis                                                                       |
|-------------|----------------------------------------------------------------|-----------------------------------------------------------------------------------|
| tenantId    | ciąg                                                         | Identyfikator dzierżawy klienta dla usługi Azure AD. Jest to również nazywane MicrosoftID. |
| domena      | ciąg                                                         | Nazwa klienta, na przykład contoso.onmicrosoft.com.                             |
| Companyname | ciąg                                                         | Nazwa firmy lub organizacji.                                          |
| Linki       | [ResourceLinks](utility-resources.md#resourcelinks)           | Linki zasobów zawarte w profilu.                                  |
| atrybuty  | [ResourceAttributes](utility-resources.md#resourceattributes) | Atrybuty metadanych odpowiadające profilowi.                             |
|organizationRegistrationNumber|Ciąg|Numer rejestracji organizacji klienta (w niektórych krajach określany również jako numer NUMER IDENTYFIKACYJNY). Wymagana tylko w przypadku firmy/organizacji klienta znajdującej się w następujących krajach: Zamówienie (AM), Kolumbia (AZ), Kolumbia (HU), KZ), Kyrgyzstan(KG), Azja (MD), Korea (RU), Tajikistan(TJ), Przemysl(UZ), Indie, Brazylia, Republika Południowej Afryki,Portal, Zjednoczone Królestwo, Arabia, Przećwicz, Wietnam, Anwil, Przemysl, Południowe Niemówiące i Ankai. W przypadku firmy/organizacji klienta znajdującej się w innych krajach nie należy tego określać.|


## <a name="customerbillingprofile"></a>CustomerBillingProfile

Zasób **CustomerBillingProfile** to dodatkowe informacje używane do rozliczenia klienta.

| Właściwość       | Typ                                                           | Opis                                                                                                                                            |
|----------------|----------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
| identyfikator             | ciąg                                                         | Identyfikator profilu.                                                                                                                                |
| firstName      | ciąg                                                         | Imię kontaktu rozliczeniowego w firmie klienta. Jest to osoba, do której będą kierowane faktury i inne informacje dotyczące rozliczeń. |
| lastName       | ciąg                                                         | Nazwisko kontaktu rozliczeniowego.                                                                                                                  |
| poczta e-mail          | ciąg                                                         | Adres e-mail kontaktu rozliczeniowego                                                                                                                    |
| kultura        | ciąg                                                         | Preferowana kultura komunikacji i waluty, taka jak "pl-pl".                                                                               |
| language       | ciąg                                                         | Preferowany język komunikacji.                                                                                                            |
| Companyname    | ciąg                                                         | Nazwa firmy lub organizacji.                                                                                                               |
| defaultAddress | [Adres](utility-resources.md#address)                       | Adres, na który są wysyłane rachunki, na który działa kontakt rozliczeniowy.                                                                                   |
| Linki          | [ResourceLinks](utility-resources.md#resourcelinks)           | Linki zasobów zawarte w profilu.                                                                                                       |
| atrybuty     | [ResourceAttributes](utility-resources.md#resourceattributes) | Atrybuty metadanych odpowiadające profilowi.                                                                                                  |

## <a name="customerrelationshiprequest"></a>CustomerRelationshipRequest

Zasób **CustomerRelationshipRequest** zawiera adres URL używany przez klienta do ustanowienia relacji odsprzedawcy z partnerem.

| Właściwość   | Typ                                                           | Opis                                                              |
|------------|----------------------------------------------------------------|--------------------------------------------------------------------------|
| url        | ciąg                                                         | Adres URL używany przez klienta do ustanowienia relacji z partnerem. |
| atrybuty | [ResourceAttributes](utility-resources.md#resourceattributes) | Atrybuty metadanych odpowiadające żądaniu relacji.       |