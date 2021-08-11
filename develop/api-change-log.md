---
title: Dziennik zmian interfejsu API REST Centrum partnerskiego
description: Ta strona zawiera listę zmian w Partner Center API REST
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.topic: reference
ms.date: 12/15/2020
ms.openlocfilehash: f74f59969bf8d73c6e6e8b39900a53c337a2af715c168b59009792beddf43159
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/06/2021
ms.locfileid: "115993286"
---
# <a name="december-2020-changes-to-partner-center-rest-apis"></a>Zmiany w interfejsach API REST Partner Center grudzień 2020 r.

Sprawdź tutaj, czy nie Partner Center interfejsów API REST.

## <a name="enhancements-to-education-pricing-eligibility-apis"></a>Ulepszenia interfejsów API uprawnień do cennika usług edukacyjnych



### <a name="what-has-changed"></a>Co się zmieniło?

Obecnie interfejs API Partner Center ma kwalifikacje GET i PUT, aby zweryfikować uprawnienia klientów z edukacji. Interfejs API kwalifikacji GET nie zostanie wprowadzony. Dodaliśmy jednak przypadek zwrotny do interfejsu API kwalifikacji PUT.

- GET — nie zmienia się.
- PUT — zostanie dodany przypadek zwrotny.

Te interfejsy API zostaną wycofane z końcem lutego 2021 r. i zostaną zastąpione przez nowe interfejsy API, zgodnie z poniższym opisem.

### <a name="scenarios-impacted"></a>Scenariusze, których to miało wpływ:

Uprawnienia klientów do korzystania z cennika dla edukacji dla wybranych jednostki SKU

### <a name="detail-descriptions"></a>Szczegółowe opisy

Zostaną wprowadzone dwa nowe interfejsy API kwalifikacji GET i POST. Nowe interfejsy API będą używać **kwalifikacji,** a nie **kwalifikacji.** Interfejsy API będą dostępne do testowania w 2. kwartale 2. kwartału.

#### <a name="get-qualifications"></a>Kwalifikacje GET

```http
GET {customer_id}/qualifications
```

#### <a name="response-example"></a>Przykładowa odpowiedź:

```json
{
  "Qualification": "Education",
  "VettingStatus": "Denied",
  "VettingReason": "Not an education customer",
  "VettingCreatedDate": "07/09/2020: 00:00:00" //UTC
}
```

#### <a name="response-fields"></a>Pola odpowiedzi: 

- Wartości VettingStatus: Zatwierdzone, Odrzucone, InReview itp.

- Wartości VettingReason:
   - Nie jest klientem edukacyjnym
   - Nie ma już klienta edukacyjnego
   - Nie jest klientem edukacyjnym — po przeglądzie
   - Ograniczony jako klient edukacyjny
   - Nie jest domeną akademickią
   - Biblioteka nie jest kwalifikowana
   - Nie kwalifikuje się do pomocy
 
#### <a name="post-qualifications"></a>Kwalifikacje POST

```http
POST {customer_id}/qualifications
    [
            "Qualification": "Education"
    ]
```

#### <a name="response-example"></a>Przykładowa odpowiedź:

```JSON
{
  "Qualification": "Education",
  "VettingStatus": "InReview",
  "VettingCreatedDate": "07/09/2020: 00:00:00" //UTC
}
```

## <a name="next-steps"></a>Następne kroki

[Dokumentacja interfejsu API REST Centrum partnerskiego](partner-center-rest-api-reference.md)
