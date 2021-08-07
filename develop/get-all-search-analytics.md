---
title: Pobieranie wszystkich informacji analitycznych dotyczących wyszukiwania
description: Jak uzyskać wszystkie informacje dotyczące analizy wyszukiwania.
ms.date: 06/27/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: a420752264f4d3074ba8a569c931654fda3ad6363d8d5d8b6a7a3e32af126bd1
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/06/2021
ms.locfileid: "115990906"
---
# <a name="get-all-search-analytics-information"></a>Pobieranie wszystkich informacji analitycznych dotyczących wyszukiwania

**Dotyczy:** Partner Center | Partner Center obsługiwana przez firmę 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government

Jak uzyskać wszystkie informacje analityczne dotyczące wyszukiwania dla klientów.

## <a name="prerequisites"></a>Wymagania wstępne

- Poświadczenia zgodnie z opisem w [te Partner Center uwierzytelniania.](partner-center-authentication.md) Ten scenariusz obsługuje uwierzytelnianie tylko przy użyciu poświadczeń użytkownika.

## <a name="rest-request"></a>Żądanie REST

### <a name="request-syntax"></a>Składnia żądania

| Metoda  | Identyfikator URI żądania |
|---------|-------------|
| **Pobierz** | [*\{ baseURL \}*](partner-center-rest-urls.md)/partner/v1/analytics/search HTTP/1.1 |

### <a name="uri-parameters"></a>Parametry URI

|    Parametr     |  Typ  |                                                                                                                   Opis                                                                                                                    |
|------------------|--------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|      filter      | ciąg |                                                                     Zwraca dane zgodne z warunkiem filtru. </br> **Przykład:**</br> `.../search?filter=field eq 'value'`                                                                     |
|     Groupby      | ciąg |                                         Obsługuje zarówno terminy, jak i daty. Logika obwodu krótkiego, aby ograniczyć liczbę zasobników. </br> **Przykład:**</br> `.../search?groupby=termField1,dateField1,termField2`                                         |
| aggregationLevel | ciąg | Parametr *aggregationLevel* wymaga *grupowania przez*. Parametr *aggregationLevel* ma zastosowanie do wszystkich pól daty obecnych w *grupie .* </br> **Przykład:**</br>  `.../search?groupby=termField1,dateField1,termField2&aggregationLevel=day` |
|       top (pierwsze)        | ciąg |                                                                     Limit stron wynosi 10000. Przyjmuje dowolną wartość mniejszą niż 10000.  </br> **Przykład:**</br>  `.../search?top=100`                                                                     |
|       Pomiń       | ciąg |                                                                                  Liczba wierszy do pominięcia. </br> **Przykład:**</br> `.../search?top=100&skip=100`                                                                                   |

### <a name="request-headers"></a>Nagłówki żądań

Aby uzyskać więcej informacji, [zobacz Partner Center REST headers (Nagłówki REST).](headers.md)

### <a name="request-body"></a>Treść żądania

Brak.

### <a name="request-example"></a>Przykład żądania

```http
GET https://api.partnercenter.microsoft.com/partner/v1/analytics/search HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
Content-Type: application/json
Content-Length: 0
```

## <a name="rest-response"></a>Odpowiedź REST

Jeśli to się powiedzie, treść odpowiedzi zawiera kolekcję [zasobów](partner-center-analytics-resources.md#search-resource) wyszukiwania.

### <a name="response-success-and-error-codes"></a>Kody powodzenia i błędów odpowiedzi

Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie, oraz dodatkowe informacje o debugowaniu. Użyj narzędzia śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry. Aby uzyskać pełną listę, zobacz [Kody błędów](error-codes.md).

### <a name="response-example"></a>Przykład odpowiedzi

```http
{
  "companyName": "my company",
  "contactButtonClicked": false,
  "keywordCountry": null,
  "detailsViewed": true,
  "keywordIndustryFocus": null,
  "mpnId": 2604568,
  "partnerMarket": "CN",
  "keywordProduct": null,
  "referralSubmitted": false,
  "searchDate": "2018-05-30",
  "keywordSearchText": " my company"
}
```

## <a name="see-also"></a>Zobacz też

- [Analiza Centrum partnerskiego — zasoby](partner-center-analytics-resources.md)
