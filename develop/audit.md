---
title: Inspekcja operacji Partner Center danych
description: Dowiedz się więcej o typie operacji inspekcji Partner Center API, których można użyć do uzyskania rekordu Partner Center aktywności.
ms.date: 05/21/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 0e8010bde75bee4c4954034d8f61f19b076d96349e4a05807e272ca88efbc2fa
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/06/2021
ms.locfileid: "115994272"
---
# <a name="audit-operations-available-via-partner-center-api-that-show-a-record-of-partner-center-activity"></a>Operacje inspekcji dostępne za Partner Center API, które pokazują rekord Partner Center aktywności

Interfejsy PARTNER CENTER zapewniają funkcje inspekcji, dzięki czemu można uzyskać rekord Partner Center aktywności.

Rekordy inspekcji z ostatnich 30 dni można pobrać od bieżącej daty lub dla zakresu dat określonego przez uwzględnienia daty rozpoczęcia i/lub daty zakończenia. Należy jednak pamiętać, że ze względu na wydajność dostępność danych dziennika aktywności jest ograniczona do 90 poprzednich dni. Żądania z datą rozpoczęcia większą niż 90 dni przed bieżącą datą otrzymają wyjątek złego żądania (kod błędu: 400) i odpowiedni komunikat.

## <a name="retrieve-audit-records"></a>Pobieranie rekordów inspekcji

Pobierz szczegółowe historyczne rekordy inspekcji operacji wykonywanych przez użytkownika lub aplikację partnera:

- [Pobieranie rejestru aktywności w Centrum partnerskim](get-a-record-of-partner-center-activity-by-user.md)
- [Inspekcja zasobów](auditing-resources.md)