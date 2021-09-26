---
title: Pobiera pojedynczą promocję
description: Pobiera pojedynczą promocję dla danego identyfikatora i kraju.
ms.date: 09/23/2021
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: BrentSerbus
ms.author: brserbus
ms.openlocfilehash: 9ed9171cd7bbe8a6d5202deb7cc6111bb76ec923
ms.sourcegitcommit: 7be22de808a10fa2d05577d6497086c8ca3f678a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/24/2021
ms.locfileid: "128715995"
---
# <a name="get-promotion-by-id"></a>Uzyskiwanie promocji według identyfikatora

**Dotyczy**

- Centrum partnerskie

**Odpowiednie role**

- Administrator globalny
- Agent administracyjny

> [!Note] 
> Nowe zmiany handlowe są obecnie dostępne tylko dla partnerów, którzy są częścią nowego Microsoft 365 i dynamics 365 w wersji Technical Preview.

Partnerzy mogą uzyskać pojedynczą promocję dla danego identyfikatora i kraju promocji. Ta metoda zwraca dane promocji, ignorując daty rozpoczęcia i zakończenia promocji. Ta metoda jest używana głównie do celów uzgadniania w celu pobrania szczegółów promocji nawet po wygaśnięciu promocji.



## <a name="prerequisites"></a>Wymagania wstępne

- Poświadczenia zgodnie z opisem w te [Partner Center uwierzytelniania.](partner-center-authentication.md) Ten scenariusz obsługuje uwierzytelnianie przy użyciu zarówno poświadczeń aplikacji autonomicznej, jak i aplikacji i użytkownika.

- Identyfikator promocji jest rozdzielany zestawem ciągów, które reprezentują określonego promocji.

- Kraj reprezentuje, dla których są dostępne promocje dla kraju klienta. Country (Kraj) jest reprezentowany przez dwu znakowy kod kraju.

## <a name="rest-request"></a>Żądanie REST

### <a name="request-syntax"></a>Składnia żądania

| Metoda   | Identyfikator URI żądania                                                                                                                         |
|----------|-------------------------------------------------------------------------------------------------------------------------------------|
| **POBIERZ**  | [*{baseURL}*](partner-center-rest-urls.md)/v1/productpromotions/{identyfikator-promocji}?country={kod-kraju HTTP/1.1 |

### <a name="uri-parameter"></a>Parametr URI

Użyj następujących parametrów zapytania, aby zwrócić dostępne promocje.

| Nazwa                    | Typ     | Wymagane | Opis                                       |
|-------------------------|----------|----------|---------------------------------------------------|
| **identyfikator promocji**  | **ciąg** | Y        | Ciąg definiujący podciąg do pobrania.           |
| **Kraju** | **ciąg** | Y        | Dwulitowy kod kraju określający, dla którego kraju klienta są dostępne promocje. |

### <a name="request-headers"></a>Nagłówki żądań

Aby uzyskać więcej informacji, [zobacz Partner Center REST headers (Nagłówki REST).](headers.md)

### <a name="request-body"></a>Treść żądania

Brak

### <a name="request-example"></a>Przykład żądania

```http
GET https://api.partnercenter.microsoft.com/v1/productpromotions/CFQ7TTC0HD33:0003:CFQ7TTC0K59M?country=US HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 18752a69-1aa1-4ef7-8f9d-eb3681b2d70a
MS-CorrelationId: 81b08ffe-4cf8-49cd-82db-5c2fb0a8e132
X-Locale: en-US
```

## <a name="rest-response"></a>Odpowiedź REST

Jeśli to się powiedzie, ta metoda zwraca jeden podystuł.

### <a name="response-success-and-error-codes"></a>Kody powodzenia i błędów odpowiedzi

Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie, oraz więcej informacji o debugowaniu. Użyj narzędzia śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry. Aby uzyskać pełną listę, zobacz [Kody błędów](error-codes.md).

### <a name="response-example"></a>Przykład odpowiedzi

```http
HTTP/1.1 200 OK
Content-Length: 138
Content-Type: application/json
MS-CorrelationId: 81b08ffe-4cf8-49cd-82db-5c2fb0a8e132
MS-RequestId: 18752a69-1aa1-4ef7-8f9d-eb3681b2d70a
Date: Fri, 24 Sep 2021 20:42:26 GMT

 
        {
            "id": "39NFJQT1PJQB:0001:39NFJQT1Q5KN",
            "name": "Visio Plan 1",
            "description": "Visio Plan 1",
            "startDate": "2021-09-23T00:00:00+00:00",
            "endDate": "2021-10-14T23:59:59+00:00",
            "properties": {
                "isAutoApplicable": true
            },
            "requiredProducts": [
                {
                    "productId": "CFQ7TTC0HD33",
                    "skuId": "0003",
                    "term": {
                        "duration": "P1Y",
                        "billingCycle": "Annual"
                    },
                    "pricingPolicies": [
                        {
                            "policyType": "PercentDiscount",
                            "value": "0.05"
                        }
                    ]
                }
            ]
        }
```
