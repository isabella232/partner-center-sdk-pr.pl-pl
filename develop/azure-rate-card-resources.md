---
title: Karta stawki platformy Azure — bieżące ceny platformy Azure
description: Dowiedz się, jak korzystać z karty Azure Rate Card, aby uzyskać aktualne ceny ofert platformy Azure w czasie rzeczywistym w Twoim regionie. Dostęp do karty Azure Rate Card można uzyskać za pośrednictwem Partner Center API REST.
ms.date: 05/21/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: amitravat
ms.author: amrava
ms.openlocfilehash: e0b1bc9d764e2132315205653f46cef73b25e02f
ms.sourcegitcommit: ad8082bee01fb1f57da423b417ca1ca9c0df8e45
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/10/2021
ms.locfileid: "111974339"
---
# <a name="azure-rate-card-resources-to-get-real-time-current-azure-prices-on-azure-offers-in-your-region"></a>Zasoby kart stawki platformy Azure do uzyskania bieżących cen platformy Azure w czasie rzeczywistym w ofertach platformy Azure w Twoim regionie

**Dotyczy:** Partner Center | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government

Karta Azure Rate Card zapewnia ceny ofert platformy Azure w czasie rzeczywistym. Cennik platformy Azure jest dynamiczny i często się zmienia. Firma Microsoft publikuje aktualizacje w Partner Center, ale interfejs API REST zapewnia najszybszy sposób na Dostawca rozwiązań w chmurze partnerów w celu uzyskania bieżących cen.

Aby śledzić użycie i ułatwić przewidywanie miesięcznego rachunku i rachunku dla poszczególnych klientów, możesz połączyć zapytanie Karta stawki w celu uzyskania cen dla usługi [Microsoft Azure](get-prices-for-microsoft-azure.md) z żądaniem uzyskania rekordów wykorzystania klienta dla platformy [Azure.](get-a-customer-s-utilization-record-for-azure.md)

Ceny różnią się w zależności od rynku i waluty, a ten interfejs API uwzględnia lokalizację. Domyślnie interfejs API używa ustawień profilu partnera w języku Partner Center i języku przeglądarki, a te ustawienia można dostosowywać. Świadomość lokalizacji jest szczególnie przydatna, jeśli zarządzasz sprzedażą na wielu rynkach z jednego, scentralizowanego biura.

## <a name="azureratecard"></a>AzureRateCard

Opisuje właściwości zasobu karty stawki platformy Azure.

| Właściwość      | Typ                                      | Opis                                                       |
|---------------|-------------------------------------------|-------------------------------------------------------------------|
| currency      | ciąg                                    | Waluta, w której są podane stawki.                     |
| isTaxIncluded | boolean                                   | Wszystkie stawki są przedzadaniowe, więc ta właściwość zwraca wartość `false` . |
| locale        | ciąg                                    | Kultura, w której informacje o zasobie są zlokalizowane.       |
| Metrów        | tablica obiektów                          | Tablica [obiektów AzureMeter.](#azuremeter)                       |
| offerTerms    | tablica obiektów                          | Tablica [obiektów AzureOfferTerm.](#azureofferterm)               |
| atrybuty    | [ResourceAttributes](utility-resources.md#resourceattributes) | Atrybuty metadanych. Zawiera `"objectType": "AzureRateCard"`   |

### <a name="operations-on-the-azureratecard-resource"></a>Operacje na zasobie AzureRateCard

- [Pobieranie cen platformy Microsoft Azure](get-prices-for-microsoft-azure.md)

## <a name="azuremeter"></a>AzureMeter

| Właściwość         | Typ             | Opis                                                                                   |
|------------------|------------------|-----------------------------------------------------------------------------------------------|
| identyfikator               | ciąg           | Unikatowy identyfikator miernika.                                                                    |
| name             | ciąg           | Przyjazna nazwa miernika.                                                                   |
| stawki            | object           | Stawki mierników. Kluczem jest ilość miernika (ciąg), a wartością jest stawka miernika (liczba). |
| tags             | tablica ciągów | Opcjonalne tagi mierników. Ta tablica może być pusta.                                                 |
| category         | ciąg           | Kategoria zasobu.                                                                     |
| Podkategorii      | ciąg           | Podkategoria zasobu.                                                                 |
| region           | ciąg           | Region identyfikatora.                                                                             |
| unit             | ciąg           | Typ ilości (godziny, bajty itp.)                                                     |
| includedQuantity | liczba           | Ilość miernika, która jest bezpłatna.                                               |
| effectiveDate    | ciąg           | Data, na która jest obowiązywał ten miernik.                                                             |

## <a name="azureofferterm"></a>AzureOfferTerm

| Właściwość         | Typ             | Opis                             |
|------------------|------------------|-----------------------------------------|
| name             | ciąg           | Przyjazna nazwa terminu oferty.        |
| discount         | liczba           | Rabat zastosowany, jeśli został zastosowany.           |
| excludedMeterIds | tablica ciągów | Mierniki wykluczone z oferty, jeśli są. |
| effectiveDate    | ciąg           | Data wejścia w życie oferty.        |
