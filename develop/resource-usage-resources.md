---
title: Zasoby rekordów użycia zasobów
description: Zasobu ResourceUsageRecord można użyć do opisania szacowanego kosztu pieniężnego użycia poziomu zasobów subskrypcji w bieżącym cyklu rozliczeniowym.
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: b0a28620eec86e86630aef93b13f26c9dd675a5d
ms.sourcegitcommit: faea78fe3264cbafc2b02c04d98d5ce30e992124
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/03/2021
ms.locfileid: "106274567"
---
# <a name="resource-usage-record-resources"></a>Zasoby rekordów użycia zasobów

**Dotyczy:**

- Centrum partnerskie

Zasobu **ResourceUsageRecord** można użyć do opisania szacowanego kosztu pieniężnego użycia poziomu zasobów subskrypcji w bieżącym cyklu rozliczeniowym.

## <a name="resourceusagerecord"></a>ResourceUsageRecord

| Właściwość          | Typ               | Opis                                                                                                                                                                                                |
|-------------------|--------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| SubscriptionId    | ciąg             | Pobiera lub ustawia identyfikator subskrypcji. W przypadku subskrypcji Microsoft Azure (MS-AZR-0145P) ta wartość jest identyfikatorem subskrypcji commerce. W przypadku planów platformy Azure ta wartość jest identyfikatorem planu platformy Azure). |
| ResourceUri       | ciąg             | Pobiera lub ustawia identyfikator URI zasobu ".                                                                                                                                                                            |
| ResourceType      | ciąg             | Pobiera lub ustawia typ zasobu.                                                                                                                                                                            |
| EntitlementId     | ciąg             | Pobiera lub ustawia identyfikator uprawnienia (Identyfikator subskrypcji platformy Azure).                                                                                                                               |
| Uprawnienie   | ciąg             | Pobiera lub ustawia nazwę uprawnienia.                                                                                                                                                                         |
| ResourceGroupName | double             | Pobiera lub ustawia nazwę grupy zasobów.                                                                                                                                                                      |
| Nazwa              | ciąg             | Nazwa zasobu.                                                                                                                                                                                  |
| ResourceName      | ciąg             | Pobiera lub ustawia nazwę zasobu.                                                                                                                                                                     |
| TotalCost         | decimal            | Pobiera lub ustawia szacowane całkowite użycie kosztów.                                                                                                                                                               |
| CurrencyCode      | ciąg             | Pobiera lub ustawia kod waluty.                                                                                                                                                                            |
| USDTotalCost      | decimal            | Pobiera lub ustawia Szacowany łączny koszt w USD.                                                                                                                                                              |
| LastModifiedDate  | ciąg             | Dzień (w formacie daty i godziny), w którym ten rekord został ostatnio zmodyfikowany.                                                                                                                                          |
| Atrybuty        | ResourceAttributes | Atrybuty metadanych odpowiadające zasobowi.                                                                                                                                                     |
