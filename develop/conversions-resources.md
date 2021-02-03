---
title: Zasoby konwersji
description: Dowiedz się więcej o korzystaniu z zasobów konwersji interfejsu API Centrum partnerskiego, które ułatwiają konwertowanie subskrypcji próbnej na płatną subskrypcję.
ms.date: 05/23/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: d3ade5a5af76e7c637962b6bfe076ac806f337bf
ms.sourcegitcommit: a25d4951f25502cdf90cfb974022c5e452205f42
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/04/2020
ms.locfileid: "97768586"
---
# <a name="conversion-resources-to-convert-trial-subscriptions-to-paid"></a>Konwersja zasobów na potrzeby konwersji subskrypcji w wersji próbnej na płatne

**Dotyczy:**

- Centrum partnerskie
- Centrum partnerskie obsługiwane przez firmę 21Vianet
- Centrum partnerskie dla Microsoft Cloud Niemcy
- Centrum partnerskie Microsoft Cloud for US Government

Zasoby konwersji obsługują konwersję subskrypcji wersji próbnej na płatną subskrypcję.

## <a name="conversion"></a>Konwersja

Zawiera informacje służące do konwersji subskrypcji w wersji próbnej na płatną subskrypcję.

| Właściwość | Typ | Opis |
| -------- | ---- | ----------- |
| offerId | ciąg | Identyfikator oferty oryginalnej oferty wersji próbnej. |
| targetOfferId | ciąg | Identyfikator oferty dla oferty docelowej. |
| Wartooć | ciąg | Identyfikator zamówienia. |
| quantity | int | Liczba licencji. Wartość domyślna to liczba licencji w subskrypcji wersji próbnej. |
| billingCycle | ciąg | Wskazuje, jak często jest naliczana opłata za partnera w ramach subskrypcji. Możliwe wartości: **miesięcznie** (miesięcznie rozliczanych), **rocznych** (partner jest rozliczany co rok) lub **nie** (partner nie jest rozliczany. Używany do subskrypcji wersji próbnej). |

## <a name="conversionerror"></a>ConversionError

Reprezentuje błąd, który wystąpił podczas konwersji.

| Właściwość | Typ | Opis |
| -------- | ---- | ----------- |
| kod | ciąg | Kod błędu związany z problemem. Możliwe wartości: **inne** (błąd ogólny), **ConversionsNotFound** (nie można znaleźć żadnych konwersji dla subskrypcji próbnej do przekonwertowania na).
| description (opis) | ciąg | Przyjazny tekst opisujący problem. |

## <a name="conversionresult"></a>ConversionResult

Reprezentuje wynik wykonania konwersji subskrypcji.

| Właściwość       | Typ                                | Opis                                                            |
|----------------|-------------------------------------|------------------------------------------------------------------------|
| subscriptionId | ciąg                              | Identyfikator subskrypcji.                                           |
| offerId        | ciąg                              | Oryginalny identyfikator oferty.                                         |
| targetOfferId  | ciąg                              | Identyfikator oferty dla oferty docelowej.                             |
| error          | [ConversionError](#conversionerror) | Wystąpił błąd podczas próby konwersji, jeśli ma zastosowanie... |