---
title: Zasoby rekordów wykorzystania platformy Azure
description: Rekord wykorzystania platformy Azure zawiera szczegółowe informacje o wykorzystaniu zasobu subskrypcji platformy Azure.
ms.date: 08/16/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: amitravat
ms.author: amrava
ms.openlocfilehash: eb905dd41d5ab177a29bc1bd949c5eb865e4614e204250709d91f1a31304b267
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/06/2021
ms.locfileid: "115992283"
---
# <a name="azure-utilization-record-resources"></a>Zasoby rekordów wykorzystania platformy Azure

**Dotyczy:** Partner Center | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government

Rekord wykorzystania platformy Azure zawiera szczegółowe informacje o wykorzystaniu zasobu subskrypcji platformy Azure. Jeśli jesteś partnerem dostawcy usług w chmurze, który jest właścicielem relacji rozliczeń dla subskrypcji platformy Azure klientów, możesz użyć tego interfejsu API REST, aby zapewnić skalowalny sposób śledzenia użycia w ramach subskrypcji w celu wysyłania faktur do klientów na koniec każdego cyklu rozliczeniowego.

Aby śledzić użycie i ułatwić przewidywanie miesięcznego rachunku oraz rachunku dla poszczególnych klientów, możesz połączyć zapytanie Rate Card w celu uzyskania cen dla usługi [Microsoft Azure](get-prices-for-microsoft-azure.md) z żądaniem uzyskania rekordów wykorzystania klienta dla platformy [Azure.](get-a-customer-s-utilization-record-for-azure.md)

Ceny różnią się w zależności od rynku i waluty, a ten interfejs API uwzględnia lokalizację. Domyślnie interfejs API używa ustawień profilu partnera w języku Partner Center i języku przeglądarki, a te ustawienia można dostosowywać. Świadomość lokalizacji jest szczególnie przydatna, jeśli zarządzasz sprzedażą na wielu rynkach z jednego, scentralizowanego biura.

## <a name="azureutilizationrecord"></a>Rekord AzureUtilizationRecord

Opisuje właściwości zasobu rekordu wykorzystania platformy Azure.

| Właściwość       | Typ                                      | Wymagane | Opis                                                                                                                                                                             |
|----------------|-------------------------------------------|----------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| usageStartTime | ciąg                                    | Tak      | Początek zakresu czasu agregacji użycia. Odpowiedź jest pogrupowana według czasu użycia (kiedy zasób został użyty, a kiedy został zgłoszony do systemu rozliczeniowego). |
| usageEndTime   | ciąg                                    | Tak      | Koniec zakresu czasu agregacji użycia. Odpowiedź jest pogrupowana według czasu użycia. Oznacza to, kiedy zasób został użyty, a kiedy został zgłoszony do systemu rozliczeniowego.   |
| zasób       | object                                    | Tak      | Zawiera obiekt [AzureResource.](#azureresource)                                                                                                                                     |
| quantity       | liczba                                    | Tak      | Ilość zużyta przez [usługę AzureResource.](#azureresource)                                                                                                                           |
| unit           | ciąg                                    | Nie       | Typ ilości (godziny, bajty itp.) Ta właściwość jest opcjonalna                                                                                                                     |
| infoFields     | object                                    | Tak      | Pary klucz-wartość szczegółów poziomu wystąpienia. Ten obiekt może być pusty.                                                                                                                    |
| Instancedata   | object                                    | Nie       | Zawiera obiekt [AzureInstanceData,](#azureinstancedata) który zawiera pary klucz-wartość szczegółów poziomu wystąpienia. Ta właściwość jest opcjonalna i może nie zostać uwzględniona.                  |
| atrybuty     | [ResourceAttributes](utility-resources.md#resourceattributes) | Tak      | Atrybuty metadanych. Zawiera "objectType": "AzureUtilizationRecord"                                                                                                                |

### <a name="operations-on-the-azureutilizationrecord-resource"></a>Operacje na zasobie AzureUtilizationRecord

- [Pobieranie rekordów dotyczących wykorzystania platformy Azure przez klienta](get-a-customer-s-utilization-record-for-azure.md)

## <a name="azureresource"></a>AzureResource

Opisuje właściwości zasobu platformy Azure.

| Właściwość    | Typ   | Wymagane | Opis                                                                         |
|-------------|--------|----------|-------------------------------------------------------------------------------------|
| identyfikator          | ciąg | Tak      | Unikatowy identyfikator zasobu platformy Azure. Znany także jako identyfikator resourceID lub identyfikator GUID zasobu. |
| name        | ciąg | Nie       | Przyjazna nazwa używanego zasobu. Ta właściwość jest opcjonalna.            |
| category    | ciąg | Nie       | Kategoria zużytego zasobu. Ta właściwość jest opcjonalna.                   |
| Podkategorii | ciąg | Nie       | Podkategoria zużytego zasobu. Ta właściwość jest opcjonalna.               |
| region      | ciąg | Nie       | Region zużytego zasobu. Ta właściwość jest opcjonalna.                     |

## <a name="azureinstancedata"></a>AzureInstanceData

Opisuje właściwości zasobu danych wystąpienia platformy Azure.

| Właściwość       | Typ             | Wymagane | Opis                                                                                                        |
|----------------|------------------|----------|--------------------------------------------------------------------------------------------------------------------|
| resourceUri    | ciąg           | Tak      | W pełni kwalifikowany identyfikator zasobu platformy Azure, który zawiera grupy zasobów i nazwę wystąpienia.                   |
| location       | ciąg           | Tak      | Region, w którym była uruchamiana usługa.                                                                               |
| partNumber     | object           | Tak      | Unikatowa przestrzeń nazw używana do identyfikowania zasobu do użytku na platformie handlowej innych firm. Ta właściwość może być pustym ciągiem. |
| Ordernumber    | liczba           | Tak      | Unikatowa przestrzeń nazw używana do identyfikowania zamówienia innej firmy na platformie handlowej. Ta właściwość może być pustym ciągiem.          |
| tags           | tablica ciągów | Nie       | Tagi zasobów określone przez użytkownika. Ta właściwość jest opcjonalna i może nie zostać uwzględniona.                            |
| additionalInfo | tablica ciągów | Nie       | Dodatkowe dane dla zasobu platformy Azure. Ta właściwość jest opcjonalna i może nie zostać uwzględniona.                          |