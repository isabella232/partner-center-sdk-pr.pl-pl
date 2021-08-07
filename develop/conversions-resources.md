---
title: Zasoby konwersji
description: Dowiedz się więcej o Partner Center konwersji interfejsu API, aby ułatwić konwersję subskrypcji wersji próbnej na płatną subskrypcję.
ms.date: 05/23/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 9e7f8985fa15f4959f3cb5a729e492bbb9f3f624a5812f5b87fc119f841dc87e
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/06/2021
ms.locfileid: "115991875"
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