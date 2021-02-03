---
title: Operacje inspekcji działania Centrum partnerskiego
description: Informacje o typie operacji inspekcji interfejsu API Centrum partnerskiego, których można użyć do pobrania rekordu działania Centrum partnerskiego.
ms.date: 05/21/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 019bebe40c43f6ee1c2ac7da381a86ca190702d4
ms.sourcegitcommit: d1104d5c27f8fb3908a87532f80c432f0147ef5d
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/13/2020
ms.locfileid: "97768537"
---
# <a name="audit-operations-available-via-partner-center-api-that-show-a-record-of-partner-center-activity"></a>Operacje inspekcji dostępne za pośrednictwem interfejsu API Centrum partnerskiego, które pokazują rekord działania Centrum partnerskiego

Interfejsy API Centrum partnerskiego zapewniają funkcje inspekcji, dzięki czemu można uzyskać rekord działania Centrum partnerskiego.

Rekordy inspekcji można pobrać z ostatnich 30 dni od bieżącej daty lub dla zakresu dat określonego przez dołączenie daty rozpoczęcia i/lub daty zakończenia. Należy jednak pamiętać, że ze względu na wydajność dostępność danych dziennika aktywności jest ograniczona do poprzednich 90 dni. Żądania z datą rozpoczęcia większą niż 90 dni przed bieżącą datą otrzymają błędny wyjątek żądania (kod błędu: 400) i odpowiedni komunikat.

## <a name="retrieve-audit-records"></a>Pobieranie rekordów inspekcji

Uzyskaj szczegółowe historyczne rekordy inspekcji operacji wykonywanych przez użytkownika lub aplikację partnera:

- [Pobieranie rejestru aktywności w Centrum partnerskim](get-a-record-of-partner-center-activity-by-user.md)
- [Inspekcja zasobów](auditing-resources.md)