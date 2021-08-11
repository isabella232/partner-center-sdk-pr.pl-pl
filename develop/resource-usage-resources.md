---
title: Zasoby rekordów użycia zasobów
description: Możesz użyć zasobu ResourceUsageRecord, aby opisać szacowany koszt pieniężny użycia na poziomie zasobów subskrypcji w bieżącym cyklu rozliczeniowym.
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: b330c49518bc12a63f2be731eef5c57884f5b15b706ce4007bbdf1a7bb8fab0e
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/06/2021
ms.locfileid: "115996941"
---
# <a name="resource-usage-record-resources"></a>Zasoby rekordów użycia zasobów

Możesz użyć zasobu **ResourceUsageRecord,** aby opisać szacowany koszt pieniężny użycia na poziomie zasobów subskrypcji w bieżącym cyklu rozliczeniowym.

## <a name="resourceusagerecord"></a>ResourceUsageRecord

| Właściwość          | Typ               | Opis                                                                                                                                                                                                |
|-------------------|--------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| SubscriptionId    | ciąg             | Pobiera lub ustawia identyfikator subskrypcji. W Microsoft Azure subskrypcji (MS-AZR-0145P) ta wartość jest identyfikatorem subskrypcji handlowej. W przypadku planów platformy Azure ta wartość to identyfikator planu platformy Azure. |
| ResourceUri       | ciąg             | Pobiera lub ustawia zasób URI".                                                                                                                                                                            |
| ResourceType      | ciąg             | Pobiera lub ustawia typ zasobu.                                                                                                                                                                            |
| EntitlementId     | ciąg             | Pobiera lub ustawia identyfikator uprawnień (identyfikator subskrypcji platformy Azure).                                                                                                                               |
| EntitlementName (Nazwa uprawnień)   | ciąg             | Pobiera lub ustawia nazwę uprawnienia.                                                                                                                                                                         |
| ResourceGroupName | double             | Pobiera lub ustawia nazwę grupy zasobów.                                                                                                                                                                      |
| Nazwa              | ciąg             | Nazwa zasobu.                                                                                                                                                                                  |
| ResourceName      | ciąg             | Pobiera lub ustawia nazwę zasobu.                                                                                                                                                                     |
| Łączny koszt         | decimal            | Pobiera lub ustawia szacowane łączne użycie kosztów.                                                                                                                                                               |
| CurrencyCode      | ciąg             | Pobiera lub ustawia kod waluty.                                                                                                                                                                            |
| USDTotalCost      | decimal            | Pobiera lub ustawia szacowany łączny koszt w USD.                                                                                                                                                              |
| LastModifiedDate  | ciąg             | Dzień (w formacie data/godzina) ostatniej modyfikacji tego rekordu.                                                                                                                                          |
| Atrybuty        | ResourceAttributes | Atrybuty metadanych odpowiadające zasobowi.                                                                                                                                                     |
