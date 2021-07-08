---
title: Zasoby licencji
description: Opisuje zasoby związane z licencjami.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 27d44f89ac89f365e77e073c425ca45ab3638c68
ms.sourcegitcommit: b307fd75e305e0a88cfd1182cc01d2c9a108ce45
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/06/2021
ms.locfileid: "111548400"
---
# <a name="license-resources"></a>Zasoby licencji

**Dotyczy:** Partner Center | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government

Opisuje zasoby związane z licencjami.

## <a name="license"></a>Licencja

Opisuje licencję użytkownika.

>[!NOTE]
>Nieobsługiwane na Partner Center obsługiwanych przez firmę 21Vianet.

| Właściwość     | Typ                                                           | Opis                                                    |
|--------------|----------------------------------------------------------------|----------------------------------------------------------------|
| servicePlans | tablica zasobów usługi ServicePlan                                 | Kolekcja planów usług, które odpowiadają licencji |
| productSKU   | ProductSku                                                     | SKU produktu, który odpowiada licencji.        |
| atrybuty   | [ResourceAttributes](utility-resources.md#resourceattributes) | Atrybuty metadanych odpowiadające licencji.          |

## <a name="licenseupdate"></a>LicenseUpdate

Zawiera informacje używane do przypisywania lub usuwania licencji od użytkownika.

| Właściwość         | Typ                                                           | Opis                                               |
|------------------|----------------------------------------------------------------|-----------------------------------------------------------|
| licensestoAssign | tablica obiektów                                               | Tablica [obiektów LicenseAssignment.](#licenseassignment) |
| licensesToRemove | tablica ciągów                                               | Identyfikatory jednostki SKU produktu licencji do usunięcia.    |
| licenseWarnings  | tablica obiektów                                               | Tablica [obiektów LicenseWarning.](#licensewarning)       |
| atrybuty       | [ResourceAttributes](utility-resources.md#resourceattributes) | Atrybuty metadanych.                                  |

## <a name="licenseassignment"></a>Przypisanie licencji

Zawiera informacje potrzebne do operacji aktualizacji licencji.

| Właściwość      | Typ             | Opis                                                                |
|---------------|------------------|----------------------------------------------------------------------------|
| excludedPlans | tablica ciągów | Identyfikatory planu usługi, które mają być wykluczone z dostępności dla użytkownika. |
| skuId         | ciąg           | Identyfikator jednostki SKU produktu dla licencji.                                |

## <a name="licensewarning"></a>LicenseWarning

Zawiera informacje ostrzegawcze, które wystąpiły podczas operacji aktualizacji licencji.

| Właściwość     | Typ             | Opis                                         |
|--------------|------------------|-----------------------------------------------------|
| kod         | ciąg           | Kod ostrzegawczy.                                   |
| message      | ciąg           | Komunikat ostrzegawczy.                                |
| servicePlans | tablica ciągów | Nazwy planów usług skojarzone z ostrzeżeniem. |

## <a name="productsku"></a>ProductSku

Opisuje szczegóły produktu.

| Właściwość       | Typ             | Opis                                         |
|----------------|------------------|-----------------------------------------------------|
| identyfikator             | ciąg           | Identyfikator produktu.                             |
| name           | ciąg           | Identyfikator podmiotu zabezpieczeń użytkownika.                      |
| skuPartNumber  | ciąg           | Nazwa numeru części SKU produktu. Na przykład w przypadku Office 365 E3 ta wartość to `EnterprisePack` . Tej właściwości można użyć w miejsce identyfikatora, jeśli identyfikator jest niedostępny.                |
| Targettype     | ciąg           | Typ docelowy produktu. Ta właściwość określa, czy produkt ma zastosowanie do obiektu `User` , czy . `Tenant`                                                                    |
| licenseGroupId | ciąg           | Identyfikuje za pomocą identyfikatora grupy urząd lub usługę, która zarządza licencją productSku. Produkty są podzielone na grupy licencji w celu lepszego zarządzania.<br/><br/>                                                                                     `group1`— Wszystkie produkty, których licencje mogą być zarządzane przez Azure Active Directory (AAD).<br/><br/>                                            `group2`— Minecraft licencji produktu.                                         |

## <a name="serviceplan"></a>Plan usługi

Identyfikuje usługę, która można wdrożyć w ramach sku produktu. Produkt może mieć wiele planów usług.

| Właściwość         | Typ   | Opis                                                                                                       |
|------------------|--------|-------------------------------------------------------------------------------------------------------------------|
| identyfikator               | ciąg | Identyfikator planu usługi.                                                                                      |
| displayName      | ciąg | Zlokalizowanej nazwy wyświetlanej planu usługi.                                                                  |
| Servicename      | ciąg | Nazwa usługi.                                                                                                 |
| capabilityStatus | ciąg | Stan planu usługi.                                                                      |
| Targettype       | ciąg | Docelowy typ planu usługi. Ta właściwość określa, czy produkt ma zastosowanie do "użytkownika", czy "dzierżawy". |

## <a name="subscribedsku"></a>SubscribedSku

Opisuje subskrybowany produkt należący do dzierżawy.

| Właściwość         | Typ                                                           | Opis                                                                                       |
|------------------|----------------------------------------------------------------|---------------------------------------------------------------------------------------------------|
| availableUnits   | liczba całkowita                                                        | Liczba jednostek dostępnych do przypisania. Ta wartość jest obliczana jako całkowita liczba jednostek — zużyte jednostki. |
| activeUnits      | liczba całkowita                                                        | Liczba jednostek aktywnych do przypisania.                                                        |
| consumedUnits    | liczba całkowita                                                        | Liczba zużytych jednostek.                                                                     |
| suspendedUnits   | liczba całkowita                                                        | Liczba wstrzymanych jednostek.                                                                    |
| totalUnits       | liczba całkowita                                                        | Całkowita liczba jednostek. Ta wartość jest obliczana jako suma aktywnych i ostrzegawczych jednostek.         |
| warningUnits     | liczba całkowita                                                        | Liczba jednostek ostrzegawczych.                                                                      |
| productSku       | ProductSku                                                     | SKU produktu.                                                                                  |
| servicePlans     | tablica zasobów usługi ServicePlan                                 | Kolekcja planów usług produktu.                                                     |
| capabilityStatus | ciąg                                                         | Stan sku produktu.                                                                      |
| atrybuty       | [ResourceAttributes](utility-resources.md#resourceattributes) | Atrybuty metadanych odpowiadające zasobowi.                                            |
