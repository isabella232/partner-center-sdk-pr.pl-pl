---
title: Zasoby rekordów użycia zasobów
description: Możesz użyć zasobu ResourceUsageRecord, aby opisać szacowany koszt pieniężny użycia na poziomie zasobów subskrypcji w bieżącym cyklu rozliczeniowym.
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: eb626b9d4cb4c57a07f45bcf7b914f534e62ab68
ms.sourcegitcommit: 0b2a62af1765a447addd9c4340c28bc42fdc2747
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/04/2021
ms.locfileid: "111446585"
---
# <a name="resource-usage-record-resources"></a>Zasoby rekordów użycia zasobów

Możesz użyć zasobu **ResourceUsageRecord,** aby opisać szacowany koszt pieniężny użycia na poziomie zasobów subskrypcji w bieżącym cyklu rozliczeniowym.

## <a name="resourceusagerecord"></a>ResourceUsageRecord

| Właściwość          | Typ               | Opis                                                                                                                                                                                                |
|-------------------|--------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| SubscriptionId    | ciąg             | Pobiera lub ustawia identyfikator subskrypcji. W Microsoft Azure subskrypcji (MS-AZR-0145P) ta wartość jest identyfikatorem subskrypcji handlowej. W przypadku planów platformy Azure ta wartość jest identyfikatorem planu platformy Azure). |
| ResourceUri       | ciąg             | Pobiera lub ustawia URI zasobu."                                                                                                                                                                            |
| ResourceType      | ciąg             | Pobiera lub ustawia typ zasobu.                                                                                                                                                                            |
| EntitlementId     | ciąg             | Pobiera lub ustawia identyfikator uprawnień (identyfikator subskrypcji platformy Azure).                                                                                                                               |
| EntitlementName   | ciąg             | Pobiera lub ustawia nazwę uprawnienia.                                                                                                                                                                         |
| ResourceGroupName | double             | Pobiera lub ustawia nazwę grupy zasobów.                                                                                                                                                                      |
| Nazwa              | ciąg             | Nazwa zasobu.                                                                                                                                                                                  |
| ResourceName      | ciąg             | Pobiera lub ustawia nazwę zasobu.                                                                                                                                                                     |
| Łączny koszt         | decimal            | Pobiera lub ustawia szacowane łączne użycie kosztów.                                                                                                                                                               |
| CurrencyCode      | ciąg             | Pobiera lub ustawia kod waluty.                                                                                                                                                                            |
| USDTotalCost      | decimal            | Pobiera lub ustawia szacowany łączny koszt w USD.                                                                                                                                                              |
| LastModifiedDate  | ciąg             | Dzień (w formacie data/godzina), w przypadku których ten rekord został ostatnio zmodyfikowany.                                                                                                                                          |
| Atrybuty        | ResourceAttributes | Atrybuty metadanych odpowiadające zasobowi.                                                                                                                                                     |
