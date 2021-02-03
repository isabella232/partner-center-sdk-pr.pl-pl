---
title: Zasoby profilu
description: Opisuje zachowanie profilów dostawcy rozwiązań w chmurze.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: e0561278995f4f9747320866b51de57efea8f712
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/19/2020
ms.locfileid: "97768317"
---
# <a name="profile-resources"></a>Zasoby profilu

**Dotyczy**

- Centrum partnerskie
- Centrum partnerskie obsługiwane przez firmę 21Vianet
- Centrum partnerskie dla Microsoft Cloud Niemcy
- Centrum partnerskie Microsoft Cloud for US Government

Opisuje zachowanie profilów dostawcy rozwiązań w chmurze.

## <a name="billingprofile"></a>BillingProfile

Opisuje profil rozliczeń partnera.

| Właściwość            | Typ                                                           | Opis                                                 |
|---------------------|----------------------------------------------------------------|-------------------------------------------------------------|
| companyName         | ciąg                                                         | Nazwa firmy rozliczenia.                                   |
| adres             | [Adres](utility-resources.md#address)                       | Adres rozliczeniowy firmy lub organizacji. |
| primaryContact      | [Kontakt](utility-resources.md#contact)                       | Podstawowy kontakt dotyczący firmy lub organizacji.        |
| purchaseOrderNumber | ciąg                                                         | Numer zamówienia zakupu firmy lub organizacji.        |
| Taksówka               | ciąg                                                         | Identyfikator podatkowy firmy lub organizacji.                       |
| billingCurrency     | ciąg                                                         | Waluta używana przez firmę lub organizację.           |
| plik profiletype         | ciąg                                                         | Typ profilu partnera.                                   |
| linki               | [ResourceLinks](utility-resources.md#resourcelinks)           | Linki do zasobów powiązane z profilem.            |
| atrybuty          | [ResourceAttributes](utility-resources.md#resourceattributes) | Atrybuty metadanych odpowiadające profilowi.       |

## <a name="legalbusinessprofile"></a>LegalBusinessProfile

Opisuje firmowy profil biznesowy partnera.

| Właściwość               | Typ                                                           | Opis                                                                                                                                                          |
|------------------------|----------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| companyName            | ciąg                                                         | Nazwa firmy prawnej.                                                                                                                                              |
| adres                | [Adres](utility-resources.md#address)                       | Adres firmy lub organizacji.                                                                                                                          |
| primaryContact         | [Kontakt](utility-resources.md#contact)                       | Podstawowy kontakt dotyczący firmy lub organizacji.                                                                                                                 |
| companyApproverAddress | [Adres](utility-resources.md#address)                       | Adres osoby zatwierdzającej firmy.                                                                                                                                        |
| companyApproverEmail   | ciąg                                                         | Adres e-mail osoby zatwierdzającej firmy.                                                                                                                                          |
| vettingStatus          | ciąg                                                         | Stan przed sprawdzeniem. Ta wartość jest reprezentacją ciągu dla jednej z nazw składowych znalezionych w [**VettingStatus**](/dotnet/api/microsoft.store.partnercenter.models.partners.vettingstatus).           |
| vettingSubStatus       | ciąg                                                         | Stan podrzędny przed sprawdzeniem. Ta wartość jest reprezentacją ciągu dla jednej z nazw składowych znalezionych w [**VettingSubStatus**](/dotnet/api/microsoft.store.partnercenter.models.partners.vettingsubstatus). |
| plik profiletype            | ciąg                                                         | Typ profilu partnera.                                                                                                                                            |
| linki                  | [ResourceLinks](utility-resources.md#resourcelinks)           | Linki do zasobów powiązane z profilem.                                                                                                                     |
| atrybuty             | [ResourceAttributes](utility-resources.md#resourceattributes) | Atrybuty metadanych odpowiadające profilowi.                                                                                                                |

## <a name="mpnprofile"></a>MpnProfile

Opisuje profil Microsoft Partner Network partnera.

| Właściwość    | Typ                                                           | Opis                                           |
|-------------|----------------------------------------------------------------|-------------------------------------------------------|
| partnerName | ciąg                                                         | Nazwa firmy lub organizacji.                     |
| mpnId       | ciąg                                                         | Identyfikator Microsoft Partner Network.                     |
| plik profiletype | ciąg                                                         | Typ profilu partnera.                             |
| linki       | [ResourceLinks](utility-resources.md#resourcelinks)           | Linki do zasobów powiązane z profilem.      |
| atrybuty  | [ResourceAttributes](utility-resources.md#resourceattributes) | Atrybuty metadanych odpowiadające profilowi. |

## <a name="organizationprofile"></a>OrganizationProfile

Opisuje profil organizacji partnera.

| Właściwość       | Typ                                                           | Opis                                                            |
|----------------|----------------------------------------------------------------|------------------------------------------------------------------------|
| identyfikator             | ciąg                                                         | Identyfikator organizacji.                                                 |
| companyName    | ciąg                                                         | Nazwa firmy lub organizacji.                               |
| defaultAddress | [Adres](utility-resources.md#address)                       | Domyślny adres firmy lub organizacji.                    |
| tenantId       | ciąg                                                         | Identyfikator dzierżawy.                                                 |
| domena         | ciąg                                                         | Domena firmy lub organizacji.                                  |
| poczta e-mail          | ciąg                                                         | Pobiera lub ustawia subskrypcję nadrzędną.                                  |
| language       | ciąg                                                         | Preferowany język komunikacji.                              |
| kultura        | ciąg                                                         | Preferowana kultura do komunikacji i waluty, na przykład "en-us". |
| plik profiletype    | ciąg                                                         | Typ profilu partnera.                                              |
| linki          | [ResourceLinks](utility-resources.md#resourcelinks)           | Linki do zasobów powiązane z profilem.                       |
| atrybuty     | [ResourceAttributes](utility-resources.md#resourceattributes) | Atrybuty metadanych odpowiadające profilowi.                  |

## <a name="supportprofile"></a>SupportProfile

Opisuje profil obsługi partnera.

| Właściwość    | Typ                                                           | Opis                                           |
|-------------|----------------------------------------------------------------|-------------------------------------------------------|
| poczta e-mail       | ciąg                                                         | Adres e-mail skojarzony z profilem.        |
| telefon   | ciąg                                                         | Numer telefonu skojarzony z profilem.         |
| witryna internetowa     | ciąg                                                         | Witryna sieci Web pomocy technicznej.                                  |
| plik profiletype | ciąg                                                         | Typ profilu partnera.                             |
| linki       | [ResourceLinks](utility-resources.md#resourcelinks)           | Linki do zasobów powiązane z profilem.      |
| atrybuty  | [ResourceAttributes](utility-resources.md#resourceattributes) | Atrybuty metadanych odpowiadające profilowi. |

