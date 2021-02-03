---
title: Pobieranie wszystkich informacji analitycznych dotyczących poleceń
description: Jak uzyskać wszystkie informacje analityczne dotyczące odwołań.
ms.date: 06/27/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: Kim-Davis
ms.author: kimnich
ms.openlocfilehash: b470c59cecf8b214e6d90a244e928e5d15ebd3e0
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/08/2020
ms.locfileid: "97767929"
---
# <a name="get-all-referrals-analytics-information"></a>Pobieranie wszystkich informacji analitycznych dotyczących poleceń

**Dotyczy**

- Centrum partnerskie
- Centrum partnerskie dla Microsoft Cloud Niemcy
- Centrum partnerskie Microsoft Cloud for US Government

Jak uzyskać wszystkie informacje o analizie odwołań dla swoich klientów.

## <a name="prerequisites"></a>Wymagania wstępne

- Poświadczenia zgodnie z opisem w temacie [uwierzytelnianie w centrum partnerskim](partner-center-authentication.md). Ten scenariusz obsługuje tylko uwierzytelnianie z poświadczeniami użytkownika.

## <a name="rest-request"></a>Żądanie REST

### <a name="request-syntax"></a>Składnia żądania

| Metoda  | Identyfikator URI żądania |
|---------|-------------|
| **Pobierz** | [*\{ BASEURL \}*](partner-center-rest-urls.md)/partner/V1/Analytics/Referrals http/1.1 |

### <a name="uri-parameters"></a>Parametry identyfikatora URI

| Parametr | Typ | Opis |
|-----------|------|-------------|
| filter | ciąg | Zwraca dane pasujące do warunku filtru.</br> **Przykład:**</br>  `.../referrals?filter=field eq 'value'` |
| GroupBy | ciąg | Obsługuje zarówno warunki, jak i daty. Algorytm krótkiego obwodu ograniczający liczbę przedziałów.</br> **Przykład:**</br>  `.../referrals?groupby=termField1,dateField1,termField2` |
| aggregationLevel | ciąg | Parametr *aggregationLevel* wymaga elementu *GroupBy*. Parametr *aggregationLevel* ma zastosowanie do wszystkich pól daty znajdujących się w *GroupBy*.</br> **Przykład:**</br> `.../referrals?groupby=termField1,dateField1,termField2&aggregationLevel=day` |
| top (pierwsze) | ciąg | Limit stron to 10000. Przyjmuje dowolną wartość mniejszą niż 10000.</br> **Przykład:**</br> `.../referrals?top=100`</br> |
| Pomiń | ciąg | Liczba wierszy do pominięcia.</br> **Przykład:**</br>  `.../referrals?top=100&skip=100` |

### <a name="request-headers"></a>Nagłówki żądań

Aby uzyskać więcej informacji, zobacz [nagłówki REST Centrum partnerskiego](headers.md).

### <a name="request-body"></a>Treść żądania

Brak.

### <a name="request-example"></a>Przykład żądania

```http
GET https://api.partnercenter.microsoft.com/partner/v1/analytics/referrals HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
Content-Type: application/json
Content-Length: 0
```

## <a name="rest-response"></a>Odpowiedź REST

Jeśli to się powiedzie, treść odpowiedzi zawiera kolekcję zasobów [odwołań](partner-center-analytics-resources.md#referrals-resource) .

### <a name="response-success-and-error-codes"></a>Kody sukcesu i błędów odpowiedzi

Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie i dodatkowe informacje debugowania. Użyj narzędzia do śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry. Aby uzyskać pełną listę, zobacz [kody błędów](error-codes.md).

### <a name="response-example"></a>Przykład odpowiedzi

```http
{
  "id": "112310",
  "status": "Accepted",
  "customerMarket": "US",
  "customerName": "Best Customer Ever",
  "customerOrgSize": "10to50employees",
  "acceptedDate": "2018-02-07T23:43:19",
  "acknowledgedDate": "2018-02-07T23:40:50",
  "archivedDate": null,
  "declinedDate": null,
  "expiredDate": null,
  "lostDate": null,
  "missedDate": null,
  "createdDate": "2018-02-04T23:08:59",
  "skippedDate": null,
  "wonDate": null,
  "partnerMarket": "US"
}
```

## <a name="see-also"></a>Zobacz też

- [Analiza Centrum partnerskiego — zasoby](partner-center-analytics-resources.md)
