---
title: Zasoby rekordów użycia platformy Azure
description: Rekord użycia platformy Azure zawiera szczegółowe informacje dotyczące użycia zasobu subskrypcji platformy Azure.
ms.date: 08/16/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: amitravat
ms.author: amrava
ms.openlocfilehash: 21d39c4497c00f5abeeeb771dfe20cd1e2b1c13a
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/08/2020
ms.locfileid: "97767762"
---
# <a name="azure-utilization-record-resources"></a>Zasoby rekordów użycia platformy Azure

**Dotyczy:**

- Centrum partnerskie
- Centrum partnerskie dla Microsoft Cloud Niemcy
- Centrum partnerskie Microsoft Cloud for US Government

Rekord użycia platformy Azure zawiera szczegółowe informacje dotyczące użycia zasobu subskrypcji platformy Azure. Jeśli jesteś partnerem dostawcy usług w chmurze, który jest właścicielem relacji rozliczeń dla subskrypcji platformy Azure, możesz użyć tego interfejsu API REST, aby zapewnić skalowalny sposób śledzenia użycia w ramach subskrypcji w celu wysłania faktury do klientów na końcu każdego cyklu rozliczeniowego.

Aby śledzić użycie i pomóc w przewidywaniu miesięcznych opłat i rachunków dla poszczególnych klientów, możesz połączyć zapytanie dotyczące karty stawki w celu [uzyskania cen za Microsoft Azure](get-prices-for-microsoft-azure.md) z żądaniem [uzyskania rekordów użycia klienta na platformie Azure](get-a-customer-s-utilization-record-for-azure.md).

Ceny różnią się w zależności od rynku i waluty, a ten interfejs API przyjmuje lokalizację. Domyślnie interfejs API używa ustawień profilu partnera w centrum partnerskim i w języku przeglądarki. te ustawienia można dostosować. Rozpoznawanie lokalizacji jest szczególnie istotne w przypadku zarządzania sprzedażą na wielu rynkach z jednego, scentralizowanego biura.

## <a name="azureutilizationrecord"></a>AzureUtilizationRecord

Opisuje właściwości zasobu rekordu użycia platformy Azure.

| Właściwość       | Typ                                      | Wymagane | Opis                                                                                                                                                                             |
|----------------|-------------------------------------------|----------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| usageStartTime | ciąg                                    | Tak      | Początek zakresu czasu agregacji użycia. Odpowiedź jest pogrupowana według czasu użycia (gdy zasób był faktycznie używany, a kiedy był raportowany do systemu rozliczeń). |
| usageEndTime   | ciąg                                    | Tak      | Koniec zakresu czasu agregacji użycia. Odpowiedź jest pogrupowana według czasu użycia. Oznacza to, że gdy zasób był faktycznie używany, a kiedy był raportowany do systemu rozliczeń.   |
| zasób       | object                                    | Tak      | Zawiera obiekt [AzureResource](#azureresource) .                                                                                                                                     |
| quantity       | liczba                                    | Tak      | Ilość zużyta przez [AzureResource.](#azureresource)                                                                                                                           |
| unit           | ciąg                                    | Nie       | Typ ilości (godziny, bajty itp.) Ta właściwość jest opcjonalna                                                                                                                     |
| infoFields     | object                                    | Tak      | Pary klucz-wartość szczegółów poziomu wystąpienia. Ten obiekt może być pusty.                                                                                                                    |
| instanceData   | object                                    | Nie       | Zawiera obiekt [AzureInstanceData](#azureinstancedata) , który zawiera pary klucz-wartość szczegółów poziomu wystąpienia. Ta właściwość jest opcjonalna i może nie być uwzględniona.                  |
| atrybuty     | [ResourceAttributes](utility-resources.md#resourceattributes) | Tak      | Atrybuty metadanych. Zawiera "objectType": "AzureUtilizationRecord"                                                                                                                |

### <a name="operations-on-the-azureutilizationrecord-resource"></a>Operacje na zasobie AzureUtilizationRecord

- [Pobieranie rekordów dotyczących wykorzystania platformy Azure przez klienta](get-a-customer-s-utilization-record-for-azure.md)

## <a name="azureresource"></a>AzureResource

Opisuje właściwości zasobu platformy Azure.

| Właściwość    | Typ   | Wymagane | Opis                                                                         |
|-------------|--------|----------|-------------------------------------------------------------------------------------|
| identyfikator          | ciąg | Tak      | Unikatowy identyfikator zasobu platformy Azure. Znany również jako resourceID lub identyfikator GUID zasobu. |
| name        | ciąg | Nie       | Przyjazna nazwa zużywanego zasobu. Ta właściwość jest opcjonalna.            |
| category    | ciąg | Nie       | Kategoria użytego zasobu. Ta właściwość jest opcjonalna.                   |
| podkategorii | ciąg | Nie       | Podkategoria użytego zasobu. Ta właściwość jest opcjonalna.               |
| region      | ciąg | Nie       | Region zużywanego zasobu. Ta właściwość jest opcjonalna.                     |

## <a name="azureinstancedata"></a>AzureInstanceData

Opisuje właściwości zasobu danych wystąpienia platformy Azure.

| Właściwość       | Typ             | Wymagane | Opis                                                                                                        |
|----------------|------------------|----------|--------------------------------------------------------------------------------------------------------------------|
| resourceUri    | ciąg           | Tak      | W pełni kwalifikowany identyfikator zasobu platformy Azure, który obejmuje grupy zasobów i nazwę wystąpienia.                   |
| location       | ciąg           | Tak      | Region, w którym uruchomiono usługę.                                                                               |
| partNumber     | object           | Tak      | Unikatowy obszar nazw używany do identyfikowania zasobu do użycia w komercyjnej witrynie Marketplace innych firm. Ta właściwość może być pustym ciągiem. |
| orderNumber    | liczba           | Tak      | Unikatowy obszar nazw używany do identyfikowania zamówienia innej firmy dla komercyjnej witryny Marketplace. Ta właściwość może być pustym ciągiem.          |
| tags           | tablica ciągów | Nie       | Tagi zasobów określone przez użytkownika. Ta właściwość jest opcjonalna i może nie być uwzględniona.                            |
| additionalInfo | tablica ciągów | Nie       | Dodatkowe dane dla zasobu platformy Azure. Ta właściwość jest opcjonalna i może nie być uwzględniona.                          |