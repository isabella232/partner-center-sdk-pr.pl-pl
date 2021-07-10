---
title: Dziennik zmian interfejsu API REST Centrum partnerskiego
description: Ta strona zawiera listę zmian w Partner Center API REST
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.topic: reference
ms.date: 12/15/2020
ms.openlocfilehash: d4f7f034a36a26b6219086ca952b189f7a313ef7
ms.sourcegitcommit: 51237e7e98d71a7e0590b4d6a4034b6409542126
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/09/2021
ms.locfileid: "113571999"
---
# <a name="december-2020-changes-to-partner-center-rest-apis"></a>Zmiany w interfejsach API REST Partner Center grudniu 2020 r.

Sprawdź tutaj, czy nie Partner Center interfejsów API REST.

## <a name="enhancements-to-education-pricing-eligibility-apis"></a>Ulepszenia interfejsów API uprawnień do cennika edukacji



### <a name="what-has-changed"></a>Co się zmieniło?

Obecnie interfejs API Partner Center ma kwalifikacje GET i PUT w celu zweryfikowania uprawnień klientów z edukacji. Interfejs API kwalifikacji GET nie zostanie wprowadzony. Dodaliśmy jednak przypadek zwrotny do interfejsu API kwalifikacji PUT.

- GET — nie zmienia się.
- PUT — zostanie dodany przypadek zwrotny.

Te interfejsy API zostaną wycofane z końcem lutego 2021 r. i zostaną zastąpione przez nowe interfejsy API, zgodnie z poniższym opisem.

### <a name="scenarios-impacted"></a>Scenariusze, których to miało wpływ:

Kwalifikowalność klientów do cen usług edukacyjnych dla wybranych jednostki SKU

### <a name="detail-descriptions"></a>Szczegółowe opisy

Zostaną wprowadzone dwa nowe interfejsy API kwalifikacji GET i POST. Nowe interfejsy API będą używać **kwalifikacji,** a nie **kwalifikacji.** Interfejsy API będą dostępne do testowania w 2. kwartale roku 2. kwartału.

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

- Wartości VettingStatus: Approved, Denied, InReview itp.

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
