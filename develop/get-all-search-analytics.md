---
title: Pobieranie wszystkich informacji analitycznych dotyczących wyszukiwania
description: Jak uzyskać wszystkie informacje dotyczące usługi Search Analytics.
ms.date: 06/27/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 967f8d0ed2d276e0f68a047204b64d83dc69da95
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/08/2020
ms.locfileid: "97767713"
---
# <a name="get-all-search-analytics-information"></a>Pobieranie wszystkich informacji analitycznych dotyczących wyszukiwania

**Dotyczy**

- Centrum partnerskie
- Centrum partnerskie obsługiwane przez firmę 21Vianet
- Centrum partnerskie dla Microsoft Cloud Niemcy
- Centrum partnerskie Microsoft Cloud for US Government

Jak uzyskać wszystkie informacje o analizie wyszukiwania dla swoich klientów.

## <a name="prerequisites"></a>Wymagania wstępne

- Poświadczenia zgodnie z opisem w temacie [uwierzytelnianie w centrum partnerskim](partner-center-authentication.md). Ten scenariusz obsługuje tylko uwierzytelnianie z poświadczeniami użytkownika.

## <a name="rest-request"></a>Żądanie REST

### <a name="request-syntax"></a>Składnia żądania

| Metoda  | Identyfikator URI żądania |
|---------|-------------|
| **Pobierz** | [*\{ BASEURL \}*](partner-center-rest-urls.md)/partner/V1/Analytics/Search http/1.1 |

### <a name="uri-parameters"></a>Parametry identyfikatora URI

|    Parametr     |  Typ  |                                                                                                                   Opis                                                                                                                    |
|------------------|--------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|      filter      | ciąg |                                                                     Zwraca dane pasujące do warunku filtru. </br> **Przykład:**</br> `.../search?filter=field eq 'value'`                                                                     |
|     GroupBy      | ciąg |                                         Obsługuje zarówno warunki, jak i daty. Algorytm krótkiego obwodu ograniczający liczbę przedziałów. </br> **Przykład:**</br> `.../search?groupby=termField1,dateField1,termField2`                                         |
| aggregationLevel | ciąg | Parametr *aggregationLevel* wymaga elementu *GroupBy*. Parametr *aggregationLevel* ma zastosowanie do wszystkich pól daty znajdujących się w *GroupBy*. </br> **Przykład:**</br>  `.../search?groupby=termField1,dateField1,termField2&aggregationLevel=day` |
|       top (pierwsze)        | ciąg |                                                                     Limit stron to 10000. Przyjmuje dowolną wartość mniejszą niż 10000.  </br> **Przykład:**</br>  `.../search?top=100`                                                                     |
|       Pomiń       | ciąg |                                                                                  Liczba wierszy do pominięcia. </br> **Przykład:**</br> `.../search?top=100&skip=100`                                                                                   |

### <a name="request-headers"></a>Nagłówki żądań

Aby uzyskać więcej informacji, zobacz [nagłówki REST Centrum partnerskiego](headers.md).

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

Jeśli to się powiedzie, treść odpowiedzi zawiera kolekcję zasobów [wyszukiwania](partner-center-analytics-resources.md#search-resource) .

### <a name="response-success-and-error-codes"></a>Kody sukcesu i błędów odpowiedzi

Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie i dodatkowe informacje debugowania. Użyj narzędzia do śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry. Aby uzyskać pełną listę, zobacz [kody błędów](error-codes.md).

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
