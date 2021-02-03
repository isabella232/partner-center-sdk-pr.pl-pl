---
title: Zasoby uaktualniania produktu
description: Do planu platformy Azure można użyć wielu zasobów związanych z uaktualnieniami produktów w centrum partnerskim. Obejmują one ProductUpgradeRequest, ProductUpgradesEligibility, ProductUpgradesStatus, UpgradesLineItem, UpgradeProduct i ErrorDetails.
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: c0245141dc99832f47bff9b68741724d5d313ab8
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/08/2020
ms.locfileid: "97767798"
---
# <a name="product-upgrade-resources"></a>Zasoby uaktualniania produktu

**Dotyczy:**

- Centrum partnerskie

Korzystając z poniższych zasobów, można uzyskać informacje o uaktualnieniach produktów Centrum partnerskiego z subskrypcji Microsoft Azure (MS-AZR-0145P) do planu platformy Azure.

## <a name="productupgraderequest"></a>ProductUpgradeRequest

Zasób **ProductUpgradesRequest** zawiera informacje o obiekcie żądanie aktualizacji produktu.

| Właściwość | Typ | Opis |
|----------------------|----------------------------------------------|----------------------------------------------------------------|
| customerId           | ciąg                                       | Ciąg sformatowany przez identyfikator GUID, który identyfikuje klienta. |
| productFamily        | ciąg                                       | Rodzina produktów, dla której zażądano uaktualnienia. |
| atrybuty           | [ResourceAttributes](utility-resources.md#resourceattributes) | Atrybuty metadanych. |

## <a name="productupgradeseligibility"></a>ProductUpgradesEligibility

Zasób **ProductUpgradesEligibility** zawiera informacje o uprawnieniach klienta do uaktualniania produktu.

| Właściwość | Typ | Opis |
|----------------------|--------------------------------------------- |----------------------------------------------------------------|
| customerId           | ciąg                                       | Ciąg sformatowany przez identyfikator GUID, który identyfikuje klienta. |          | productFamily        | ciąg                                       | Rodzina produktów, dla której zażądano uaktualnienia. |
| nie kwalifikuj           | bool                                         | Wartość logiczna wskazuje, czy klient kwalifikuje się do żądanego uaktualnienia. |
| upgradeId            | ciąg                                       | Identyfikator uaktualnienia w przypadku, gdy uaktualnienie produktu dla danej rodziny już istnieje. |
| reason               | ciąg                                       | Powód, dla którego klient nie kwalifikuje się do uaktualnienia produktu. |
| productFamily        | ciąg                                       | Rodzina produktów, dla której zażądano uaktualnienia. |
| atrybuty           | [ResourceAttributes](utility-resources.md#resourceattributes) | Atrybuty metadanych.

## <a name="productupgradesstatus"></a>ProductUpgradesStatus

Zasób **ProductUpgradesStatus** zawiera informacje o stanie uaktualnienia produktu.

| Właściwość | Typ | Opis |
|---------------------|----------------------------------------------------------------|-----------------------------------------------|
| Id                  | ciąg                                                         | Ciąg w formacie GUID, który identyfikuje uaktualnienie. |
| productFamily       | ciąg                                                         | Rodzina produktów, dla której zażądano uaktualnienia.
| status              | ciąg                                                         | Stan uaktualnienia produktu.
| lineItems           | Tablica zasobów [UpgradesLineItem](#upgradeslineitem)       | Tablica obiektów, która zawiera informacje o szczegółach uaktualnienia dla każdego elementu wiersza, który był częścią treści żądania.
| errorDetails        | Zasób [ErrorDetails](#errordetails)                         | Szczegóły błędu dla żądania uaktualnienia.
| atrybuty          | [ResourceAttributes](utility-resources.md#resourceattributes)  | Atrybuty metadanych. |

## <a name="upgradeslineitem"></a>UpgradesLineItem

Zasób **UpgradesLineItem** opisuje stan szczegółów uaktualnienia produktu dla każdego elementu wiersza żądania.

| Właściwość | Typ | Opis |
|-----------------|-----------------------------------------------------|--------------------------------------------------------------|
| sourceProduct   | Obiekt [UpgradeProduct](#upgradeproduct)            | Informacje o uaktualnianym produkcie źródłowym. |
| targetProduct   | Obiekt [UpgradeProduct](#upgradeproduct)            | Informacje o docelowym uaktualnieniu produktu. |
| upgradedDate    | ciąg w formacie daty i godziny UTC                      | Data uaktualnienia subskrypcji. |
| status          | ciąg                                              | Stan uaktualnienia produktu. |
| errorDetails    | Zasób [ErrorDetails](#errordetails)              | Szczegóły błędu dla żądania uaktualnienia. |
| atrybuty      | [ResourceAttributes](utility-resources.md#resourceattributes) | Atrybuty metadanych.  |

## <a name="upgradeproduct"></a>UpgradeProduct

Zasób **UpgradeProduct** zawiera informacje o uaktualnianym produkcie.

| Właściwość | Typ |Opis |
|----------------------|----------------------------------------------|----------------------------------------------------------------|
| identyfikator                   | ciąg                                       | Ciąg w formacie GUID, który identyfikuje produkt. |
| name                 | ciąg                                       | Przyjazna nazwa produktu, który jest uaktualniany. |
| atrybuty           | [ResourceAttributes](utility-resources.md#resourceattributes) | Atrybuty metadanych. |

## <a name="errordetails"></a>ErrorDetails

Zasób **ErrorDetails** zawiera szczegółowe informacje o błędach podczas procesu uaktualniania.

| Właściwość | Typ | Opis |
|-------------------------|----------------------------------------------|-------------------------------------------------------------|
| kod                    | ciąg                                       | Kod błędu, gdy uaktualnienie produktu nie powiodło się. |
| message                 | ciąg                                       | Komunikat o błędzie podczas uaktualniania produktu kończy się niepowodzeniem. |
| atrybuty              | [ResourceAttributes](utility-resources.md#resourceattributes) | Atrybuty metadanych. |
