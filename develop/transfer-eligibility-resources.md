---
title: Przenoszenie zasobów uprawnień
description: Partner może utworzyć przeniesienie, gdy klient zażąda, aby jego subskrypcja została przeniesiona do innego partnera.
ms.date: 04/10/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 8f121d499abffb4c4dda688c2a91c25f83d2e863
ms.sourcegitcommit: 4275f9f67f9479ce27af6a9fda96fe86d0bc0b44
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/05/2021
ms.locfileid: "111530212"
---
# <a name="transfereligibility-resources"></a>Przenoszenie zasobów uprawnień

Partner może utworzyć przeniesienie, gdy klient zażąda, aby jego subskrypcja została przeniesiona do innego partnera. Użyj uprawnienia do przeniesienia, aby sprawdzić, czy subskrypcja kwalifikuje się do przeniesienia.

## <a name="transfereligibility"></a>Uprawnienia do przeniesienia

Opisuje uprawnienie do przeniesienia.

| Właściwość              | Typ             | Opis                                                                              |
|-----------------------|------------------|------------------------------------------------------------------------------------------|
| identyfikator                    | ciąg           | Identyfikator subskrypcji klienta.                                                  |
| isEligible            | bool             | Wskazuje, czy subskrypcja kwalifikuje się do przeniesienia.                         |
| Przyczyna                | ciąg           | Właściwość przyczyny wyjaśnia, dlaczego subskrypcja nie kwalifikuje się do przeniesienia. |