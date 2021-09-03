---
title: Zasoby przejściowe
description: Opisuje zasoby używane do przechodzenia nowych subskrypcji handlowych.
ms.date: 02/23/2021
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: BrentSerbus
ms.author: brserbus
ms.openlocfilehash: 44867be3823414ab43957e789c0cd29aef44d956
ms.sourcegitcommit: e1db965e8c7b4fe3aaa0ecd6cefea61973ca2232
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/03/2021
ms.locfileid: "123457308"
---
# <a name="transition-resources"></a>Zasoby przejściowe

**Dotyczy**

- Centrum partnerskie

**Odpowiednie role**

- Administrator globalny
- Agent administracyjny

> [!Note] 
> Nowe zmiany w handlu są obecnie dostępne tylko dla partnerów, którzy są częścią nowego doświadczenia handlowego M365/D365 w wersji Technical Preview.

Opisuje zasoby używane do przejścia z jednej nowej subskrypcji handlowej do innej.

## <a name="transitioneliblity"></a>TransitionEliblity

Opisuje zachowanie zasobu przejścia indywidualnej subskrypcji.

| Właściwość          | Typ                    | Opis                                                                                  |
|-------------------|-------------------------|----------------------------------------------------------------------------------------------|
| CatalogItemId | ciąg                  | Identyfikator elementu katalogu, dla których jest sprawdzany. |
| Tytuł  | ciąg                  | Tytuł SKU. |
| Opis | ciąg                  | Opis sku. |
| Liczba | liczba całkowita                 | Ilość nowej oferty do zakupienia. |
| Uprawnienia | lista transitioneligibilityDetail | Lista szczegółów uprawnień do przejścia. | 

## <a name="transitioneligibilitydetail"></a>TransitionEligibilityDetail

Opisuje zachowanie zasobu szczegółów uprawnień do poszczególnych przejść.

| Właściwość          | Typ                    | Opis                                                                                  |
|-------------------|-------------------------|----------------------------------------------------------------------------------------------|
| IsEligible | boolean | Zwraca uprawnienie jest prawidłowe lub nie. |
| TransitionType | TransitionType | Typ przejścia. Mogą być transition_with_license_transfer lub transition_only. |
| błędy | Lista elementów TransitionErrors | Atrybuty metadanych odpowiadające błędowi. |

## <a name="transition"></a>Transition

Opisuje zachowanie zasobu przejścia indywidualnej subskrypcji.

| Właściwość          | Typ                    | Opis                                                                                  |
|-------------------|-------------------------|----------------------------------------------------------------------------------------------|
| FromCatalogItemId | ciąg                  | Identyfikator elementu z katalogu. |
| ToCatalogItemId   | ciąg                  | Identyfikator elementu wykazu do. |
| ToSubscriptionId  | ciąg                  | Identyfikator subskrypcji Do. Jest on wypełniany tylko w przypadku zmiany subskrypcji. Obecnie jest to potrzebne tylko w przypadku starszego uaktualnienia, ale nowoczesne przejście częściowe również będzie potrzebne. |
| Liczba          | liczba całkowita                 | Ilość, która jest przenoszona do elementu katalogu docelowego. |
| TransitionType    | ciąg              | Typ przejścia. Możliwe wartości — transition_only, transition_with_license_transfer.   |
| Zdarzenia            | lista elementów TransitionEvents | Zdarzenia przejścia. |

## <a name="transitionevent"></a>TransitionEvent

Opisuje przyczynę, dla których nie można wykonać uaktualnienia.

| Właściwość          | Typ               | Opis                                                                                                                                                                                                                                                                                                                                                                                     |
|-------------------|--------------------|------------------------------------------------------------------------------|
| Nazwa | ciąg | Nazwa zdarzenia przejścia. Możliwe wartości konwersji lub LicenseReassignment. |
| Stan | ciąg  | Stan zdarzenia przejścia. Możliwe wartości InProgress, Completed lub Failed.  |
| Znacznik czasu | DateTime | Sygnatura czasowa UTC zdarzenia. |
| błędy | Lista elementów TransitionErrors | Atrybuty metadanych odpowiadające błędowi. |

## <a name="transitionerror"></a>TransitionError

Reprezentuje błąd uprawnień do przeniesienia subskrypcji. Zawiera przyczynę, dla których nie można wykonać przejścia.

| Właściwość          | Typ               | Opis                                                                                                                                                                                                                                                                                                                                                                                     |
|-------------------|--------------------|--------------------------------------------------------------|
| Kod | TransitionErrorCode | Kod błędu skojarzony z problemem. |
| Opis | ciąg  | Przyjazny tekst opisujący błąd. |

