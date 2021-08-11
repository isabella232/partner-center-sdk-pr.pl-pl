---
title: Przenoszenie zasobów uprawnień
description: Partner może utworzyć przeniesienie, gdy klient zażąda, aby jego subskrypcja została przeniesiona do innego partnera.
ms.date: 04/10/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: ffe72aa04de17cf6e45e49e9fdbec8ba08da2deed89f5d54425a17825c91a53a
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/06/2021
ms.locfileid: "115996652"
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