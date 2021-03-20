---
title: Dziennik zmian interfejsu API REST Centrum partnerskiego
description: Ta strona zawiera zmiany w interfejsie API REST Centrum partnerskiego
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.topic: reference
ms.date: 12/15/2020
ms.openlocfilehash: b2c2cac36a8bd1bec7aa5bf6e5d1aa73b4779535
ms.sourcegitcommit: 717e483a6eec23607b4e31ddfaa3e2691f3043e6
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 03/20/2021
ms.locfileid: "104711852"
---
# <a name="december-2020-changes-to-partner-center-rest-apis"></a>Grudzień 2020 zmiany w interfejsie API REST Centrum partnerskiego

Tutaj znajdziesz zmiany w interfejsie API REST Centrum partnerskiego.

## <a name="enhancements-to-education-pricing-eligibility-apis"></a>Ulepszenia dotyczące interfejsów API kwalifikowania się do cen edukacyjnych



### <a name="what-has-changed"></a>Co się zmieniło?

Obecnie interfejs API Centrum partnerskiego ma uprawnienia do uzyskiwania kwalifikacji w celu zweryfikowania kwalifikacji klientów edukacyjnych. Nie zostaną wprowadzone żadne zmiany w interfejsie API pobierania kwalifikacji. Jednak dodaliśmy przypadek powrotu do interfejsu API UMIESZCZAnia kwalifikacji.

- GET-nie zmienia. [Bieżący artykuł interfejsu API](./get-customer-qualification-synchronous.md)
- Przypadek do zwrócenia zostanie dodany. [Bieżący artykuł interfejsu API](./update-customer-qualification-synchronous.md)

Te interfejsy API zostaną wycofane na koniec lutego 2021, aby zostały zastąpione przez nowe interfejsy API, zgodnie z poniższym opisem.

### <a name="scenarios-impacted"></a>Wpływ na scenariusze:

Kwalifikowanie klientów do cen edukacyjnych na wybranych jednostkach SKU

### <a name="detail-descriptions"></a>Opisy szczegółów

Zostaną wprowadzone dwa nowe interfejsy API pobierania i ZAMIESZCZAnia kwalifikacji. Nowe interfejsy API będą korzystać z **kwalifikacji**, a nie **kwalifikacji**. Interfejsy API będą dostępne do testowania w FY21 Q2.

#### <a name="get-qualifications"></a>Pobierz kwalifikacje

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

- VettingStatus wartości: zatwierdzone, odrzucone, Nieprzejrzane itp.

- VettingReason wartości:
   - Nie jest to klient edukacyjny
   - Nie jest już klientem edukacyjnym
   - Nie jest to klient edukacyjny — po przeprowadzeniu przeglądu
   - Ograniczony jako klient edukacyjny
   - Nie jest to domena edukacyjna
   - To nie jest kwalifikująca się biblioteka
   - Nie kwalifikuje się muzeów
 
#### <a name="post-qualifications"></a>Ogłoś kwalifikacje

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