---
title: Zasoby licencji
description: Opisuje zasoby związane z licencjami.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 681f53ec73122a4861e6f1a2f96560336481a068
ms.sourcegitcommit: d53d300dc7fb01aeb4ef85bf2e3a6b80f868dc57
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/14/2020
ms.locfileid: "97768198"
---
# <a name="license-resources"></a>Zasoby licencji

**Dotyczy**

- Centrum partnerskie
- Centrum partnerskie dla Microsoft Cloud Niemcy
- Centrum partnerskie Microsoft Cloud for US Government

Opisuje zasoby związane z licencjami.

## <a name="license"></a>Licencja

Opisuje licencję użytkownika.

>[!NOTE]
>Nieobsługiwane w centrum partnerskim obsługiwanym przez firmę 21Vianet.

| Właściwość     | Typ                                                           | Opis                                                    |
|--------------|----------------------------------------------------------------|----------------------------------------------------------------|
| Plany serviceplan | Tablica zasobów serviceplan                                 | Kolekcja planów usług, które odpowiadają licencji |
| productSKU   | ProductSku                                                     | Jednostka SKU produktu, która odnosi się do licencji.        |
| atrybuty   | [ResourceAttributes](utility-resources.md#resourceattributes) | Atrybuty metadanych odpowiadające licencji.          |

## <a name="licenseupdate"></a>LicenseUpdate

Zawiera informacje służące do przypisywania lub usuwania licencji od użytkownika.

| Właściwość         | Typ                                                           | Opis                                               |
|------------------|----------------------------------------------------------------|-----------------------------------------------------------|
| licensestoAssign | Tablica obiektów                                               | Tablica obiektów [LicenseAssignment](#licenseassignment) . |
| licensesToRemove | tablica ciągów                                               | Identyfikatory jednostki SKU produktu licencji do usunięcia.    |
| licenseWarnings  | Tablica obiektów                                               | Tablica obiektów [LicenseWarning](#licensewarning) .       |
| atrybuty       | [ResourceAttributes](utility-resources.md#resourceattributes) | Atrybuty metadanych.                                  |

## <a name="licenseassignment"></a>LicenseAssignment

Zawiera informacje dotyczące operacji aktualizacji licencji.

| Właściwość      | Typ             | Opis                                                                |
|---------------|------------------|----------------------------------------------------------------------------|
| excludedPlans | tablica ciągów | Identyfikatory planów usług, które mają być wykluczone z dostępności do użytkownika. |
| Identyfikatora skuId         | ciąg           | Identyfikator jednostki SKU produktu dla licencji.                                |

## <a name="licensewarning"></a>LicenseWarning

Zawiera informacje ostrzegawcze, które wystąpiły podczas operacji aktualizacji licencji.

| Właściwość     | Typ             | Opis                                         |
|--------------|------------------|-----------------------------------------------------|
| kod         | ciąg           | Kod ostrzegawczy.                                   |
| message      | ciąg           | Komunikat ostrzegawczy.                                |
| Plany serviceplan | tablica ciągów | Nazwy planów usług skojarzone z ostrzeżeniem. |

## <a name="productsku"></a>ProductSku

Opisuje szczegóły produktu.

| Właściwość       | Typ             | Opis                                         |
|----------------|------------------|-----------------------------------------------------|
| identyfikator             | ciąg           | Identyfikator produktu.                             |
| name           | ciąg           | Identyfikator podmiotu zabezpieczeń użytkownika.                      |
| skuPartNumber  | ciąg           | Nazwa jednostki SKU dla produktu. Na przykład dla pakietu Office 365 plan E3 ta wartość to `EnterprisePack` . Ta właściwość może być używana zamiast identyfikatora, jeśli identyfikator jest niedostępny.                |
| Typ     | ciąg           | Typ docelowy produktu. Ta właściwość określa, czy produkt ma zastosowanie do `User` lub `Tenant` .                                                                    |
| licenseGroupId | ciąg           | Identyfikuje za pośrednictwem identyfikatora grupy urzędu lub usługi, która zarządza licencją productSku. Produkty są segregowane pod grupą licencji, co ułatwia zarządzanie nimi.<br/><br/>                                                                                     `group1` — Wszystkie produkty, których licencje mogą być zarządzane przez Azure Active Directory (AAD).<br/><br/>                                            `group2` -Minecraft licencje na produkty.                                         |

## <a name="serviceplan"></a>Serviceplan

Identyfikuje usługę do wdrożenia w ramach jednostki SKU produktu. Produkt może mieć wiele planów usług.

| Właściwość         | Typ   | Opis                                                                                                       |
|------------------|--------|-------------------------------------------------------------------------------------------------------------------|
| identyfikator               | ciąg | Identyfikator planu usługi.                                                                                      |
| displayName      | ciąg | Zlokalizowana nazwa wyświetlana planu usługi.                                                                  |
| serviceName      | ciąg | Nazwa usługi.                                                                                                 |
| capabilityStatus | ciąg | Stan planu usługi dla planu usługi.                                                                      |
| Typ       | ciąg | Typ docelowy planu usługi. Ta właściwość określa, czy produkt ma zastosowanie do "użytkownika" lub "dzierżawy". |

## <a name="subscribedsku"></a>SubscribedSku

Opisuje subskrybowany produkt należący do dzierżawy.

| Właściwość         | Typ                                                           | Opis                                                                                       |
|------------------|----------------------------------------------------------------|---------------------------------------------------------------------------------------------------|
| availableUnits   | liczba całkowita                                                        | Liczba jednostek dostępnych do przypisania. Ta wartość jest obliczana jako łączna liczba jednostek zużytych jednostek. |
| activeUnits      | liczba całkowita                                                        | Liczba jednostek aktywnych dla przypisania.                                                        |
| consumedUnits    | liczba całkowita                                                        | Liczba zużytych jednostek.                                                                     |
| suspendedUnits   | liczba całkowita                                                        | Liczba zawieszonych jednostek.                                                                    |
| totalUnits       | liczba całkowita                                                        | Łączna liczba jednostek. Ta wartość jest obliczana jako suma jednostek aktywnych i ostrzeżeń.         |
| warningUnits     | liczba całkowita                                                        | Liczba jednostek ostrzeżeń.                                                                      |
| productSku       | ProductSku                                                     | Jednostka SKU produktu.                                                                                  |
| Plany serviceplan     | Tablica zasobów serviceplan                                 | Kolekcja planów usług produktu.                                                     |
| capabilityStatus | ciąg                                                         | Stan jednostki SKU produktu.                                                                      |
| atrybuty       | [ResourceAttributes](utility-resources.md#resourceattributes) | Atrybuty metadanych odpowiadające zasobowi.                                            |
