---
title: Zasoby konwersji
description: Dowiedz się więcej o Partner Center konwersji interfejsu API, aby ułatwić konwersję subskrypcji wersji próbnej na płatną subskrypcję.
ms.date: 05/23/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 1863c365627807d8de2534a2d3116807a5de70e1
ms.sourcegitcommit: ad8082bee01fb1f57da423b417ca1ca9c0df8e45
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/10/2021
ms.locfileid: "111973897"
---
# <a name="conversion-resources-to-convert-trial-subscriptions-to-paid"></a>Konwersja zasobów w celu konwersji subskrypcji wersji próbnej na płatną

**Dotyczy:** Partner Center | Partner Center obsługiwana przez firmę 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government

Zasoby konwersji obsługują konwersję subskrypcji wersji próbnej na płatną subskrypcję.

## <a name="conversion"></a>Konwersja

Zawiera informacje używane do konwertowania subskrypcji wersji próbnej na płatną subskrypcję.

| Właściwość | Typ | Opis |
| -------- | ---- | ----------- |
| offerId | ciąg | Identyfikator oferty oryginalnej oferty w wersji próbnej. |
| targetOfferId | ciąg | Identyfikator oferty dla oferty docelowej. |
| Idzamówienia | ciąg | Identyfikator zamówienia. |
| quantity | int | Liczba licencji. Wartość domyślna to liczba licencji w subskrypcji wersji próbnej. |
| billingCycle | ciąg | Wskazuje, jak często partner jest obciążany opłatami za subskrypcję. Możliwe wartości: **Co miesiąc** (partner jest rozliczany miesięcznie), **Roczny** (partner jest rozliczany rocznie) lub **Brak** (partner nie jest rozliczany. Używane w przypadku subskrypcji w wersji próbnej). |

## <a name="conversionerror"></a>ConversionError

Reprezentuje błąd, który wystąpił podczas konwersji.

| Właściwość | Typ | Opis |
| -------- | ---- | ----------- |
| kod | ciąg | Kod błędu skojarzony z problemem. Możliwe wartości: **Inne** (błąd ogólny), **ConversionsNotFound** (nie można znaleźć żadnych konwersji dla subskrypcji wersji próbnej, na która ma zostać przekonwertowana).
| description (opis) | ciąg | Przyjazny tekst opisujący problem. |

## <a name="conversionresult"></a>ConversionResult

Reprezentuje wynik konwersji subskrypcji.

| Właściwość       | Typ                                | Opis                                                            |
|----------------|-------------------------------------|------------------------------------------------------------------------|
| subscriptionId | ciąg                              | Identyfikator subskrypcji.                                           |
| offerId        | ciąg                              | Oryginalny identyfikator oferty.                                         |
| targetOfferId  | ciąg                              | Identyfikator oferty dla oferty docelowej.                             |
| error          | [ConversionError](#conversionerror) | Błąd napotkany podczas próby konwersji, jeśli ma zastosowanie. |