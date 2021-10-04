---
title: Pobiera historię przejścia dla wcześniej przejętej nowej subskrypcji handlowej
description: Pobiera historię przejścia dla wcześniej przejętej nowej subskrypcji handlowej.
ms.date: 02/23/2021
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: BrentSerbus
ms.author: brserbus
ms.openlocfilehash: 65859e0805397efb0c9db2f5bf566ca1b6deba49
ms.sourcegitcommit: 3ee00d9fe9da6b9df0fb7027ae506e2abe722770
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/04/2021
ms.locfileid: "129417274"
---
# <a name="get-transitions"></a>Uzyskiwanie przejść

**Dotyczy**

- Centrum partnerskie

**Odpowiednie role**

- Administrator globalny
- Agent administracyjny

> [!Note] 
> Nowe zmiany w handlu są obecnie dostępne tylko dla partnerów, którzy są częścią nowego doświadczenia handlowego M365/D365 w wersji Technical Preview.

Służy do uzyskania historii przejść dla danego klienta i subskrypcji. Historia obejmuje wszystkie zdarzenia, które zostały przetworzone w celu przejścia. Obsługuje to tylko nowe przejścia subskrypcji na podstawie licencji handlowej.

## <a name="prerequisites"></a>Wymagania wstępne

- Poświadczenia zgodnie z opisem w te [Partner Center uwierzytelniania.](partner-center-authentication.md) Ten scenariusz obsługuje uwierzytelnianie przy użyciu zarówno poświadczeń aplikacji autonomicznej, jak i aplikacji i użytkownika.

- Identyfikator klienta ( `customer-tenant-id` ). Jeśli nie znasz identyfikatora klienta, możesz go znaleźć na pulpicie nawigacyjnym Partner Center [nawigacyjnym](https://partner.microsoft.com/dashboard). Wybierz **pozycję CSP** z menu Partner Center, a następnie pozycję **Klienci.** Wybierz klienta z listy klientów, a następnie wybierz **pozycję Konto**. Na stronie Konto klienta odszukaj identyfikator **Microsoft w** sekcji **Informacje o koncie** klienta. Identyfikator microsoft jest taki sam jak identyfikator klienta ( `customer-tenant-id` ).

- Jeden identyfikator subskrypcji dla subskrypcji, która została przesłoniona.

## <a name="rest-request"></a>Żądanie REST
[GET] customers/{customer-tenant-id}/subscriptions/{subscription-id}/transitions
### <a name="request-syntax"></a>Składnia żądania

| Metoda   | Identyfikator URI żądania                                                                                                                         |
|----------|-------------------------------------------------------------------------------------------------------------------------------------|
| **POBIERZ**  | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/subscriptions/{subscription-id}/transitions HTTP/1.1 |

### <a name="uri-parameter"></a>Parametr URI

Użyj następujących parametrów zapytania, aby zwrócić kwalifikujące się przejścia.

| Nazwa                    | Typ     | Wymagane | Opis                                       |
|-------------------------|----------|----------|---------------------------------------------------|
| **identyfikator dzierżawy klienta**  | **guid** | Y        | Identyfikator GUID odpowiadający dzierżawie klienta.             |
| **subscription-id** | **guid** | Y        | Identyfikator GUID odpowiadający początkowej subskrypcji. |

### <a name="request-headers"></a>Nagłówki żądań

Aby uzyskać więcej informacji, [zobacz Partner Center REST headers (Nagłówki REST).](headers.md)

### <a name="request-body"></a>Treść żądania

Brak

### <a name="request-example"></a>Przykład żądania

```http
GET https://api.partnercenter.microsoft.com/v1/customers/{customer-tenant-id}/subscriptions/{subscription-id}/transitions HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 18752a69-1aa1-4ef7-8f9d-eb3681b2d70a
MS-CorrelationId: 81b08ffe-4cf8-49cd-82db-5c2fb0a8e132
X-Locale: en-US
```

## <a name="rest-response"></a>Odpowiedź REST

Jeśli to się powiedzie, zwraca historię przejść dla podanej subskrypcji.

### <a name="response-success-and-error-codes"></a>Kody powodzenia i błędów odpowiedzi

Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie, oraz dodatkowe informacje o debugowaniu. Użyj narzędzia śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry. Aby uzyskać pełną listę, zobacz [Kody błędów](error-codes.md).

### <a name="response-example"></a>Przykład odpowiedzi

```http
HTTP/1.1 200 OK
Content-Length: 138
Content-Type: application/json
MS-CorrelationId: 81b08ffe-4cf8-49cd-82db-5c2fb0a8e132
MS-RequestId: 18752a69-1aa1-4ef7-8f9d-eb3681b2d70a
Date: Fri, 26 Feb 2021 20:42:26 GMT

{
    "transition": [
        {
        "FromCatalogItemId": "CFQ7TTC0LDPB:0001:CFQ7TTC0LGNT",
        "ToCatalogItemId": "CFQ7TTC0LF8S:0001:CFQ7TTC0K9G9",
        "quantity": 1,
        "transitionType": "transition_with_license_transfer",
        "Events": [
           {
               "name": "Conversion",
               "status": "Started ",
               "timestamp": "2021-01-08T18:01:14.7488618Z",
               "attributes":
                     {
                          "objectType": "TransitionEvent"
                     }
           }, 
           {
               "name": "Conversion",
               "status": "Completed",
               "timestamp": "2021-01-08T18:37:41.591855Z",
               "attributes":
                     {
                          "objectType": "TransitionEvent"
                     }
            }
        ],
        "attributes":
               {
                     "objectType": "Transition"
               }
        }
    ],
    "attributes":
        {
               "objectType": "Collection"
        }
}
```

