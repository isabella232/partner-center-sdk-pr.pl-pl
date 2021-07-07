---
title: Pobieranie wszystkich informacji analitycznych dotyczących poleceń
description: Jak uzyskać wszystkie informacje analityczne dotyczące poleceń.
ms.date: 06/27/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: Kim-Davis
ms.author: kimnich
ms.openlocfilehash: 7deda4098ceb9eb4e1ee75056c53c754618bf3e2
ms.sourcegitcommit: d4b0c80d81f1d5bdf3c4c03344ad639646ae6ab9
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/09/2021
ms.locfileid: "111760610"
---
# <a name="get-all-referrals-analytics-information"></a>Pobieranie wszystkich informacji analitycznych dotyczących poleceń

**Dotyczy:** Partner Center | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government

Jak uzyskać wszystkie informacje analityczne dotyczące poleceń dla klientów.

## <a name="prerequisites"></a>Wymagania wstępne

- Poświadczenia zgodnie z opisem w te [Partner Center uwierzytelniania.](partner-center-authentication.md) Ten scenariusz obsługuje uwierzytelnianie tylko przy użyciu poświadczeń użytkownika.

## <a name="rest-request"></a>Żądanie REST

### <a name="request-syntax"></a>Składnia żądania

| Metoda  | Identyfikator URI żądania |
|---------|-------------|
| **Pobierz** | [*\{ baseURL \}*](partner-center-rest-urls.md)/partner/v1/analytics/referrals HTTP/1.1 |

### <a name="uri-parameters"></a>Parametry URI

| Parametr | Typ | Opis |
|-----------|------|-------------|
| filter | ciąg | Zwraca dane zgodne z warunkiem filtru.</br> **Przykład:**</br>  `.../referrals?filter=field eq 'value'` |
| Groupby | ciąg | Obsługuje zarówno terminy, jak i daty. Logika obwodu krótkiego ograniczająca liczbę zasobników.</br> **Przykład:**</br>  `.../referrals?groupby=termField1,dateField1,termField2` |
| aggregationLevel | ciąg | Parametr *aggregationLevel* wymaga *pogrupowania wartości*. Parametr *aggregationLevel* ma zastosowanie do wszystkich pól daty obecnych w tabeli *grupowania*.</br> **Przykład:**</br> `.../referrals?groupby=termField1,dateField1,termField2&aggregationLevel=day` |
| top (pierwsze) | ciąg | Limit stron wynosi 10000. Przyjmuje dowolną wartość mniejszą niż 10000.</br> **Przykład:**</br> `.../referrals?top=100`</br> |
| Pomiń | ciąg | Liczba wierszy do pominięcia.</br> **Przykład:**</br>  `.../referrals?top=100&skip=100` |

### <a name="request-headers"></a>Nagłówki żądań

Aby uzyskać więcej informacji, [zobacz Partner Center REST headers (Nagłówki REST).](headers.md)

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

Jeśli to się powiedzie, treść odpowiedzi zawiera kolekcję [zasobów Polecenia.](partner-center-analytics-resources.md#referrals-resource)

### <a name="response-success-and-error-codes"></a>Kody powodzenia i błędów odpowiedzi

Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie, oraz dodatkowe informacje o debugowaniu. Użyj narzędzia śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry. Aby uzyskać pełną listę, zobacz [Kody błędów](error-codes.md).

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
