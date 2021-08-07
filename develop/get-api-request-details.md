---
title: Uzyskiwanie listy wszystkich żądań użytkowników partnerów
description: Pobierz listę wszystkich żądań użytkowników partnerów przy użyciu interfejsu API REST partnera.
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.date: 05/29/2020
author: cychua
ms.author: cychua
ms.openlocfilehash: 395b21dde2790739d35e6047fbeaa7477cad50f4d1af9b12ad0b632742d71583
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/06/2021
ms.locfileid: "115990821"
---
# <a name="get-app-and-user-api-requests"></a>Uzyskiwanie żądań interfejsu API aplikacji i użytkownika

**Dotyczy:** interfejs API Partner Center API

W tym artykule wyjaśniono, jak uzyskać listę wszystkich żądań użytkowników partnerów w ramach dzierżawy przy użyciu interfejsów API REST.

 > [!NOTE]
 > Ten interfejs API zwraca tylko najnowsze żądania interfejsu API wykonane przez poświadczenia aplikacji i użytkownika z maksymalnym limitem 10 000.

## <a name="prerequisites"></a>Wymagania wstępne

- Poświadczenia zgodnie z opisem w te [Partner Center uwierzytelniania.](partner-center-authentication.md) Ten scenariusz obsługuje uwierzytelnianie przy użyciu poświadczeń aplikacji i użytkownika.

## <a name="rest-request"></a>Żądanie REST

### <a name="request-syntax"></a>Składnia żądania

| Metoda  | Identyfikator URI żądania                                                        |
|---------|--------------------------------------------------------------------|
| **Pobierz** | [*{baseURL}*](partner-center-rest-urls.md)/v1/partnerRequests |

### <a name="request-headers"></a>Nagłówki żądań

- Aby uzyskać więcej informacji, [zobacz Partner Center REST headers (Nagłówki REST).](headers.md)

### <a name="request-body"></a>Treść żądania

Brak.

### <a name="request-example"></a>Przykład żądania

```http
GET https://api.partnercenter.microsoft.com/v1/partnerRequests HTTP/1.1
Authorization: Bearer <token>
Host: api.partnercenter.microsoft.com
Content-Type: application/json
```

## <a name="rest-response"></a>Odpowiedź REST

W przypadku powodzenia ta metoda zwraca kolekcję zasobów szczegółów żądania [interfejsu API](mfa-resources.md#api-request-details) w treści odpowiedzi.

### <a name="response-success-and-error-codes"></a>Kody powodzenia i błędów odpowiedzi

Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie, oraz dodatkowe informacje o debugowaniu. Użyj narzędzia śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry. Aby uzyskać pełną listę, zobacz [Kody błędów](error-codes.md).

### <a name="response-example"></a>Przykład odpowiedzi

``` http
HTTP/1.1 200 OK
Content-Length: 2960
Content-Type: application/json
MS-CorrelationId: 4cb80cbe-566b-4d8b-8b8f-af1454b73089
MS-RequestId: 566330a7-1e4b-4848-9c23-f135c70fd810
Date: Thu, 21 May 2020 22:29:17 GMT
{
    "totalCount": 2,
    "items": [
        {
            "requestId": "6c583d8d-46cd-420c-ae3d-35b6dfdcdb21",
            "correlationId": "",
            "operationName": "Get /v{version}/nonMfaCompliantPartnerPrincipals",
            "requestDateTime": "2020-05-21T21:02:10.31",
            "sourceIpAddress": "13.88.20.150",
            "objectId": "c69854fe-5fb4-4527-a28f-f24f1acaffd6",
            "tenantId": "6e6aef4a-4ca9-40a8-b5bf-b53a1923c540",
            "upn": "admin@yourdomain.onmicrosoft.com",
            "applicationId": "60a00bf2-0644-4279-83b3-87ddf96f2509",
            "mfaCompliant": true
        },
        {
            "requestId": "09f8e434-a9ce-43ea-a9ac-270fbb22371a",
            "correlationId": "",
            "operationName": "Get /v{version}/customers/{customer_id}/subscriptions?order_id={order_id_value}&mpn_id={mpn_id_value}",
            "requestDateTime": "2020-05-21T22:18:35.73",
            "sourceIpAddress": "13.88.20.150",
            "objectId": "adc77aa5-7968-4c57-9f48-361018265c1a",
            "tenantId": "6e6aef4a-4ca9-40a8-b5bf-b53a1923c540",
            "upn": "portalnonmfa@yourdomain.onmicrosoft.com",
            "applicationId": "60a00bf2-0644-4279-83b3-87ddf96f2509",
            "mfaCompliant": false
        }
    ],
    "attributes": {
        "objectType": "Collection"
    }
}
```
