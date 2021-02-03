---
title: Karta stawka Azure — bieżące ceny platformy Azure
description: Dowiedz się, jak korzystać z karty kursu platformy Azure w celu uzyskania bieżących cen dla ofert platformy Azure w danym regionie. Dostęp do karty usługi Azure rate jest uzyskiwany za pośrednictwem interfejsu API REST Centrum partnerskiego.
ms.date: 05/21/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: amitravat
ms.author: amrava
ms.openlocfilehash: 2d011153f508ea0a745413b88003333452d0af24
ms.sourcegitcommit: d1104d5c27f8fb3908a87532f80c432f0147ef5d
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/13/2020
ms.locfileid: "97768550"
---
# <a name="azure-rate-card-resources-to-get-real-time-current-azure-prices-on-azure-offers-in-your-region"></a>Zasoby usługi Azure rate Card umożliwiające uzyskanie bieżących cen platformy Azure w czasie rzeczywistym w ramach ofert platformy Azure w Twoim regionie

**Dotyczy:**

- Centrum partnerskie
- Centrum partnerskie dla Microsoft Cloud Niemcy
- Centrum partnerskie Microsoft Cloud for US Government

Karta stawka Azure oferuje ceny w czasie rzeczywistym dla ofert platformy Azure. Cennik platformy Azure jest dość często dynamiczny i zmieniany. Firma Microsoft publikuje aktualizacje w centrum partnerskim, ale interfejs API REST zapewnia najszybszy sposób uzyskiwania bieżących cen przez partnerów dostawcy rozwiązań w chmurze.

Aby śledzić użycie i pomóc w przewidywaniu miesięcznych opłat i rachunków dla poszczególnych klientów, możesz połączyć zapytanie dotyczące karty stawki w celu [uzyskania cen za Microsoft Azure](get-prices-for-microsoft-azure.md) z żądaniem [uzyskania rekordów użycia klienta na platformie Azure](get-a-customer-s-utilization-record-for-azure.md).

Ceny różnią się w zależności od rynku i waluty, a ten interfejs API przyjmuje lokalizację. Domyślnie interfejs API używa ustawień profilu partnera w centrum partnerskim i w języku przeglądarki. te ustawienia można dostosować. Rozpoznawanie lokalizacji jest szczególnie istotne w przypadku zarządzania sprzedażą na wielu rynkach z jednego, scentralizowanego biura.

## <a name="azureratecard"></a>AzureRateCard

Opisuje właściwości zasobu karty kursu platformy Azure.

| Właściwość      | Typ                                      | Opis                                                       |
|---------------|-------------------------------------------|-------------------------------------------------------------------|
| currency      | ciąg                                    | Waluta, w której są podane stawki.                     |
| isTaxIncluded | boolean                                   | Wszystkie stawki to pretax, więc ta właściwość zwraca jako `false` . |
| locale        | ciąg                                    | Kultura, w której informacje o zasobie są zlokalizowane.       |
| Liczniki        | Tablica obiektów                          | Tablica obiektów [AzureMeter](#azuremeter) .                       |
| offerTerms    | Tablica obiektów                          | Tablica obiektów [AzureOfferTerm](#azureofferterm) .               |
| atrybuty    | [ResourceAttributes](utility-resources.md#resourceattributes) | Atrybuty metadanych. Wyświetlana `"objectType": "AzureRateCard"`   |

### <a name="operations-on-the-azureratecard-resource"></a>Operacje na zasobie AzureRateCard

- [Pobieranie cen platformy Microsoft Azure](get-prices-for-microsoft-azure.md)

## <a name="azuremeter"></a>AzureMeter

| Właściwość         | Typ             | Opis                                                                                   |
|------------------|------------------|-----------------------------------------------------------------------------------------------|
| identyfikator               | ciąg           | Unikatowy identyfikator miernika.                                                                    |
| name             | ciąg           | Przyjazna nazwa miernika.                                                                   |
| wysyłki            | object           | Stawki za metrię. Klucz jest ilością miernika (ciąg), a wartością jest stawka (liczba). |
| tags             | tablica ciągów | Opcjonalne Tagi miernika. Ta tablica może być pusta.                                                 |
| category         | ciąg           | Kategoria zasobu.                                                                     |
| podkategorii      | ciąg           | Podkategoria zasobu.                                                                 |
| region           | ciąg           | Region identyfikatora.                                                                             |
| unit             | ciąg           | Typ ilości (godziny, bajty itp.)                                                     |
| includedQuantity | liczba           | Ilość miernika, która jest oferowana bezpłatnie.                                               |
| Parametr effectivedate    | ciąg           | Data obowiązywania tego licznika.                                                             |

## <a name="azureofferterm"></a>AzureOfferTerm

| Właściwość         | Typ             | Opis                             |
|------------------|------------------|-----------------------------------------|
| name             | ciąg           | Przyjazna nazwa okresu oferty.        |
| discount         | liczba           | Zastosowano rabat (jeśli istnieje).           |
| excludedMeterIds | tablica ciągów | Liczniki wykluczone z oferty (jeśli istnieją). |
| Parametr effectivedate    | ciąg           | Data obowiązywania oferty.        |
