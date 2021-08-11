---
title: Zasoby profilu
description: Opisuje zachowanie profilów Dostawca rozwiązań w chmurze użytkownika.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 8d4c091e186b7a3ad13aee7202b3d992af95db8db50acd40a5ade496d7087359
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/06/2021
ms.locfileid: "115997315"
---
# <a name="profile-resources"></a>Zasoby profilu

**Dotyczy:** Partner Center | Partner Center obsługiwana przez firmę 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government

Opisuje zachowanie profilów Dostawca rozwiązań w chmurze użytkownika.

## <a name="billingprofile"></a>BillingProfile

Opisuje profil rozliczeniowy partnera.

| Właściwość            | Typ                                                           | Opis                                                 |
|---------------------|----------------------------------------------------------------|-------------------------------------------------------------|
| Companyname         | ciąg                                                         | Nazwa firmy rozliczeniowej.                                   |
| adres             | [Adres](utility-resources.md#address)                       | Adres rozliczeniowy firmy lub organizacji. |
| primaryContact      | [Kontakt](utility-resources.md#contact)                       | Podstawowy kontakt dla firmy lub organizacji.        |
| purchaseOrderNumber | ciąg                                                         | Numer zamówienia zakupu firmy lub organizacji.        |
| taxId               | ciąg                                                         | Identyfikator podatkowy firmy lub organizacji.                       |
| billingCurrency     | ciąg                                                         | Waluta używana przez firmę lub organizację.           |
| typ profilu         | ciąg                                                         | Typ profilu partnera.                                   |
| Linki               | [ResourceLinks](utility-resources.md#resourcelinks)           | Link zasobu odpowiadający profilowi.            |
| atrybuty          | [ResourceAttributes](utility-resources.md#resourceattributes) | Atrybuty metadanych odpowiadające profilowi.       |

## <a name="legalbusinessprofile"></a>LegalBusinessProfile

Opisuje profil biznesowy partnera z prawem.

| Właściwość               | Typ                                                           | Opis                                                                                                                                                          |
|------------------------|----------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Companyname            | ciąg                                                         | Nazwa firmy prawnej.                                                                                                                                              |
| adres                | [Adres](utility-resources.md#address)                       | Adres firmy lub organizacji.                                                                                                                          |
| primaryContact         | [Kontakt](utility-resources.md#contact)                       | Podstawowy kontakt dla firmy lub organizacji.                                                                                                                 |
| companyApproverAddress | [Adres](utility-resources.md#address)                       | Adres osoby zatwierdzającej w firmie.                                                                                                                                        |
| companyApproverEmail   | ciąg                                                         | Adres e-mail osoby zatwierdzającej w firmie.                                                                                                                                          |
| vettingStatus          | ciąg                                                         | Stan vettingu. Ta wartość jest ciągiem reprezentacji jednej z nazw członków znalezionych w [**VettingStatus**](/dotnet/api/microsoft.store.partnercenter.models.partners.vettingstatus).           |
| vettingSubStatus       | ciąg                                                         | Podstatus wytłaczania. Ta wartość jest ciągiem reprezentacji jednej z nazw członków znalezionych w [**VettingSubStatus**](/dotnet/api/microsoft.store.partnercenter.models.partners.vettingsubstatus). |
| typ profilu            | ciąg                                                         | Typ profilu partnera.                                                                                                                                            |
| Linki                  | [ResourceLinks](utility-resources.md#resourcelinks)           | Link zasobu odpowiadający profilowi.                                                                                                                     |
| atrybuty             | [ResourceAttributes](utility-resources.md#resourceattributes) | Atrybuty metadanych odpowiadające profilowi.                                                                                                                |

## <a name="mpnprofile"></a>MpnProfile

Opisuje profil Microsoft Partner Network partnera.

| Właściwość    | Typ                                                           | Opis                                           |
|-------------|----------------------------------------------------------------|-------------------------------------------------------|
| partnerName | ciąg                                                         | Nazwa firmy lub organizacji.                     |
| mpnId       | ciąg                                                         | Identyfikator Microsoft Partner Network (MPN).                     |
| typ profilu | ciąg                                                         | Typ profilu partnera.                             |
| Linki       | [ResourceLinks](utility-resources.md#resourcelinks)           | Link zasobu odpowiadający profilowi.      |
| atrybuty  | [ResourceAttributes](utility-resources.md#resourceattributes) | Atrybuty metadanych odpowiadające profilowi. |

## <a name="organizationprofile"></a>OrganizationProfile

Opisuje profil organizacji partnera.

| Właściwość       | Typ                                                           | Opis                                                            |
|----------------|----------------------------------------------------------------|------------------------------------------------------------------------|
| identyfikator             | ciąg                                                         | Identyfikator organizacji.                                                 |
| Companyname    | ciąg                                                         | Nazwa firmy lub organizacji.                               |
| defaultAddress | [Adres](utility-resources.md#address)                       | Domyślny adres firmy lub organizacji.                    |
| tenantId       | ciąg                                                         | Identyfikator dzierżawy.                                                 |
| domena         | ciąg                                                         | Domena firmy lub organizacji.                                  |
| poczta e-mail          | ciąg                                                         | Pobiera lub ustawia subskrypcję nadrzędną.                                  |
| language       | ciąg                                                         | Preferowany język komunikacji.                              |
| kultura        | ciąg                                                         | Preferowana kultura komunikacji i waluty, taka jak "pl-pl". |
| typ profilu    | ciąg                                                         | Typ profilu partnera.                                              |
| Linki          | [ResourceLinks](utility-resources.md#resourcelinks)           | Linki zasobów odpowiadające profilowi.                       |
| atrybuty     | [ResourceAttributes](utility-resources.md#resourceattributes) | Atrybuty metadanych odpowiadające profilowi.                  |

## <a name="supportprofile"></a>SupportProfile

Opisuje profil pomocy technicznej partnera.

| Właściwość    | Typ                                                           | Opis                                           |
|-------------|----------------------------------------------------------------|-------------------------------------------------------|
| poczta e-mail       | ciąg                                                         | Adres e-mail skojarzony z profilem.        |
| telefon   | ciąg                                                         | Numer telefonu skojarzony z profilem.         |
| witryna internetowa     | ciąg                                                         | Witryna sieci Web pomocy technicznej.                                  |
| typ profilu | ciąg                                                         | Typ profilu partnera.                             |
| Linki       | [ResourceLinks](utility-resources.md#resourcelinks)           | Linki zasobów odpowiadające profilowi.      |
| atrybuty  | [ResourceAttributes](utility-resources.md#resourceattributes) | Atrybuty metadanych odpowiadające profilowi. |

