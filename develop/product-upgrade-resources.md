---
title: Zasoby uaktualniania produktu
description: Możesz użyć wielu zasobów związanych z Partner Center uaktualnieniami produktu do planu platformy Azure. Należą do nich ProductUpgradeRequest, ProductUpgradesEligibility, ProductUpgradesStatus, UpgradesLineItem, UpgradeProduct i ErrorDetails.
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: c995ac44dbe22000f7bc86991cb973ed31a5c018
ms.sourcegitcommit: 0b2a62af1765a447addd9c4340c28bc42fdc2747
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/04/2021
ms.locfileid: "111445344"
---
# <a name="product-upgrade-resources"></a>Zasoby uaktualniania produktu

Poniższe zasoby zawierają informacje o uaktualnieniach produktów Partner Center z subskrypcji Microsoft Azure (MS-AZR-0145P) do planu platformy Azure.

## <a name="productupgraderequest"></a>ProductUpgradeRequest

Zasób **ProductUpgradesRequest zawiera** informacje o obiekcie żądania uaktualnień produktu.

| Właściwość      | Typ                                                          | Opis                                                |
|---------------|---------------------------------------------------------------|------------------------------------------------------------|
| customerId    | ciąg                                                        | Ciąg w formacie identyfikatora GUID, który identyfikuje klienta.      |
| productFamily | ciąg                                                        | Rodzina produktów, dla której zażądano uaktualnienia. |
| atrybuty    | [ResourceAttributes](utility-resources.md#resourceattributes) | Atrybuty metadanych.                                   |

## <a name="productupgradeseligibility"></a>ProductUpgradesEligibility

Zasób **ProductUpgradesEligibility zawiera** informacje o uprawnieniach klienta do uaktualnienia produktu.

| Właściwość      | Typ                                                          | Opis                                                                      |
|---------------|---------------------------------------------------------------|----------------------------------------------------------------------------------|
| customerId    | ciąg                                                        | Ciąg w formacie identyfikatora GUID, który identyfikuje klienta.                            |
| productFamily | ciąg                                                        | Rodzina produktów, dla której zażądano uaktualnienia.                       |
| isEligible    | bool                                                          | Wartość logiczna wskazuje, czy klient kwalifikuje się do zażądania uaktualnienia. |
| upgradeId     | ciąg                                                        | Identyfikator uaktualnienia, jeśli uaktualnienie produktu dla danej rodziny jest już na miejscu.        |
| reason        | ciąg                                                        | Przyczyna, dla której klient nie kwalifikuje się do uaktualnienia produktu.                |
| productFamily | ciąg                                                        | Rodzina produktów, dla której zażądano uaktualnienia.                       |
| atrybuty    | [ResourceAttributes](utility-resources.md#resourceattributes) | Atrybuty metadanych.                                                         |

## <a name="productupgradesstatus"></a>ProductUpgradesStatus

Zasób **ProductUpgradesStatus** zawiera informacje o stanie uaktualnienia produktu.

| Właściwość | Typ   | Opis                                          |
|----------|--------|------------------------------------------------------|
| Id       | ciąg | Ciąg w formacie identyfikatora GUID, który identyfikuje uaktualnienie. |
| productFamily       | ciąg                                                         | Rodzina produktów, dla której zażądano uaktualnienia.
| status              | ciąg                                                         | Stan uaktualnienia produktu.
| lineItems           | tablica [zasobów UpgradesLineItem](#upgradeslineitem)       | Tablica obiektów, która dostarcza informacje o szczegółach uaktualnienia dla każdego elementu wiersza, który był częścią treści żądania.
| errorDetails        | [Zasób ErrorDetails](#errordetails)                         | Szczegóły błędu dla żądanego uaktualnienia.
| atrybuty          | [ResourceAttributes](utility-resources.md#resourceattributes)  | Atrybuty metadanych. |

## <a name="upgradeslineitem"></a>UpgradesLineItem

Zasób **UpgradesLineItem** opisuje stan szczegółów uaktualnienia produktu dla każdego wiersza żądania.

| Właściwość      | Typ                                                          | Opis                                       |
|---------------|---------------------------------------------------------------|---------------------------------------------------|
| sourceProduct (źródłoProdukt) | [UpgradeProduct,](#upgradeproduct) obiekt                      | Informacje o uaktualnianych produktach źródłowych. |
| targetProduct | [UpgradeProduct,](#upgradeproduct) obiekt                      | Informacje o produkcie docelowym po uaktualnieniu.   |
| upgradedDate  | ciąg w formacie daty i czasu UTC                                | Data uaktualnienia subskrypcji.           |
| status        | ciąg                                                        | Stan uaktualnienia produktu.                |
| errorDetails  | [Zasób ErrorDetails](#errordetails)                        | Szczegóły błędu dla żądanego uaktualnienia.          |
| atrybuty    | [ResourceAttributes](utility-resources.md#resourceattributes) | Atrybuty metadanych.                          |

## <a name="upgradeproduct"></a>UpgradeProduct

Zasób **UpgradeProduct** zawiera informacje o uaktualnianych produktach.

| Właściwość   | Typ                                                          | Opis                                          |
|------------|---------------------------------------------------------------|------------------------------------------------------|
| identyfikator         | ciąg                                                        | Ciąg w formacie identyfikatora GUID, który identyfikuje produkt. |
| name       | ciąg                                                        | Przyjazna nazwa uaktualnianego produktu.         |
| atrybuty | [ResourceAttributes](utility-resources.md#resourceattributes) | Atrybuty metadanych.                             |

## <a name="errordetails"></a>ErrorDetails

Zasób **ErrorDetails** zawiera szczegółowe informacje o błędach podczas procesu uaktualniania.

| Właściwość   | Typ                                                          | Opis                                       |
|------------|---------------------------------------------------------------|---------------------------------------------------|
| kod       | ciąg                                                        | Kod błędu, gdy uaktualnienie produktu zakończy się niepowodzeniem.      |
| message    | ciąg                                                        | Komunikat o błędzie, gdy uaktualnienie produktu zakończy się niepowodzeniem. |
| atrybuty | [ResourceAttributes](utility-resources.md#resourceattributes) | Atrybuty metadanych.                          |
