---
title: Przejście nowej subskrypcji handlowej
description: Uaktualnia nową subskrypcję usługi klienta do określonej subskrypcji docelowej.
ms.date: 02/23/2021
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: BrentSerbus
ms.author: brserbus
ms.openlocfilehash: 2bbf2f63cec416e4d4b4a671d2e2b2914b5f5713
ms.sourcegitcommit: e1db965e8c7b4fe3aaa0ecd6cefea61973ca2232
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/03/2021
ms.locfileid: "123457307"
---
# <a name="transition-a-new-commerce-subscription"></a>Przejście nowej subskrypcji handlowej

**Dotyczy:** Partner Center

**Odpowiednie role**

- Administrator globalny
- Agent administracyjny

> [!Note] 
> Nowe zmiany w handlu są obecnie dostępne tylko dla partnerów, którzy są częścią nowego doświadczenia handlowego M365/D365 w wersji Technical Preview.

Służy do uaktualniania nowej subskrypcji usługi klienta do subskrypcji docelowej. Najpierw uzyskaj kwalifikujące się przejścia, aby uzyskać jednostki SKU dostępne do uaktualnienia. Następnie po przejściu w celu wykonania przejścia. Te metody obsługują zarówno tradycyjne, jak i nowe subskrypcje źródłowe handlu.  

## <a name="get-transition-eligibilities"></a>Uzyskiwanie uprawnień do przejścia

Zwraca listę kwalifikujących się przejść dla danego klienta, subskrypcji i żądanego typu.

### <a name="prerequisites"></a>Wymagania wstępne

- Poświadczenia zgodnie z opisem w te [Partner Center uwierzytelniania.](partner-center-authentication.md) Ten scenariusz obsługuje uwierzytelnianie przy użyciu zarówno poświadczeń aplikacji autonomicznej, jak i aplikacji i użytkownika.

- Identyfikator klienta ( `customer-tenant-id` ). Jeśli nie znasz identyfikatora klienta, możesz go znaleźć na pulpicie nawigacyjnym Partner Center [nawigacyjnym](https://partner.microsoft.com/dashboard). Wybierz **pozycję CSP** z menu Partner Center, a następnie pozycję **Klienci.** Wybierz klienta z listy klientów, a następnie wybierz **pozycję Konto**. Na stronie Konto klienta odszukaj identyfikator **Microsoft w** sekcji **Informacje o koncie** klienta. Identyfikator microsoft jest taki sam jak identyfikator klienta ( `customer-tenant-id` ).

- Jeden identyfikator subskrypcji dla subskrypcji początkowej.

### <a name="rest-request"></a>Żądanie REST

#### <a name="request-syntax"></a>Składnia żądania

| Metoda   | Identyfikator URI żądania                                                                                                                         |
|----------|-------------------------------------------------------------------------------------------------------------------------------------|
| **POBIERZ**  | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/subscriptions/{subscription-Id}/transitionEligibilityType?eligibilityType={immediate, scheduled} HTTP/1.1 |

#### <a name="uri-parameter"></a>Parametr URI

Użyj następujących parametrów zapytania, aby zwrócić kwalifikujące się przejścia.

| Nazwa                    | Typ     | Wymagane | Opis                                       |
|-------------------------|----------|----------|---------------------------------------------------|
| **identyfikator dzierżawy klienta**  | **guid** | Y        | Identyfikator GUID odpowiadający dzierżawie klienta.             |
| **identyfikator subscriptoin-Id** | **guid** | Y        | Identyfikator GUID odpowiadający początkowej subskrypcji. |
| **eligibilityType**       | **ciąg** | Y        | Opisuje, kiedy transcja ma zostać wykonana, może być natychmiastowa lub zaplanowana.  |

#### <a name="request-headers"></a>Nagłówki żądań

Aby uzyskać więcej informacji, [zobacz Partner Center REST headers (Nagłówki REST).](headers.md)

#### <a name="request-body"></a>Treść żądania

Brak

#### <a name="request-example"></a>Przykład żądania

```http
GET https://api.partnercenter.microsoft.com/v1/customers/{customer-tenant-id}/subscriptions/{subscription-Id}/transitionEligibilities?eligibilityType=immediate HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 18752a69-1aa1-4ef7-8f9d-eb3681b2d70a
MS-CorrelationId: 81b08ffe-4cf8-49cd-82db-5c2fb0a8e132
X-Locale: en-US
```

### <a name="rest-response"></a>Odpowiedź REST

W przypadku powodzenia ta metoda zwraca listę kwalifikujących się przejść w treści odpowiedzi.

#### <a name="response-success-and-error-codes"></a>Kody powodzenia i błędów odpowiedzi

Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie, oraz dodatkowe informacje o debugowaniu. Użyj narzędzia śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry. Aby uzyskać pełną listę, zobacz [Kody błędów](error-codes.md).

#### <a name="eligibility-errors"></a>Błędy uprawnień

Opisy błędów i ich znaczenie.

| Opis błędu | Znaczenie  |
|-------------------------|----------|
|Nie można przejść subskrypcji — subskrypcja źródłowa nie jest aktywna. | Oryginalny stan podrzędny nie jest aktywny |
|Nie można przejść subskrypcji — subskrypcja źródłowa nie została jeszcze aprowizowana. | Oryginalny sub FulfillmentState nie jest powodzenie |
|Typ przejścia nie jest zgodny — wymagane jest mapowanie subskrypcji usługi AzureAD. | Błąd LegacyCannotConvertSubscriptionId podczas wywoływania funkcji GetSubscriptionUpgradeConflicts |
|Typ przejścia nie jest zgodny — istnieją subskrypcje powodujące konflikt w przypadku przenoszenia licencji. | Jeśli dowolna usługa AAD ma identyfikatory subskrypcji z innej subskrypcji, dodaj ją do listy konfliktów (obejmuje zakupy dokonane za pomocą starszego lub nowoczesnego przepływu zakupów) |

#### <a name="response-example"></a>Przykład odpowiedzi

```http
HTTP/1.1 200 OK
Content-Length: 138
Content-Type: application/json
MS-CorrelationId: 81b08ffe-4cf8-49cd-82db-5c2fb0a8e132
MS-RequestId: 18752a69-1aa1-4ef7-8f9d-eb3681b2d70a
Date: Fri, 26 Feb 2021 20:42:26 GMT

{
    "totalCount": 2,
    "items": [
        {
            "catalogItemId": "CFQ7TTC0KZCR:0001:CFQ7TTC0K71H",
            "title": "Microsoft 365 E5 Test Sku Title",
            "description": "Microsoft 365 E5 Test Sku Description",
            "quantity": 1,
            "eligibilities": [
{
                    "isEligible": true,
                    "transitionType": "transition_only",
                    "errors": []
                },
                
{
                    "isEligible": false,
                    "transitionType": "transition_with_license_transfer",
                    "errors": [
                        {
                            "code": 3,
                            "description": "Subscription cannot be transitioned because there are conflicting services."
                        }
                    ]
                }
            ],
            "attributes": {
                "objectType": "TransitionEligibility"
            }
        },
        {
            "catalogItemId": "CFQ7TTC0L4M3:0001:CFQ7TTC0K78T",
            "title": "Business Premium Test Sku Title",
            "description": "Business Premium Test Sku Description",
            "quantity": 1,
            "eligibilities": [
                {
                    "isEligible": false,
                    "transitionType": "transition_with_license_transfer",
                    "errors": [
                        {
                            "code": 3,
                            "description": "Subscription cannot be transitioned because there are conflicting services."
                        }
                    ]
                }
            ],
            "attributes": {
                "objectType": "TransitionEligibility"
            }
        }
    ],
    "attributes": {
        "objectType": "Collection"
    }
}
```

## <a name="post-transition"></a>Po przejściu

Publikuje żądanie przejścia dla danego klienta i subskrypcji. Zwraca przejście ze stanem intial.

### <a name="prerequisites"></a>Wymagania wstępne

- Poświadczenia zgodnie z opisem w te [Partner Center uwierzytelniania.](partner-center-authentication.md) Ten scenariusz obsługuje uwierzytelnianie przy użyciu zarówno poświadczeń aplikacji autonomicznej, jak i aplikacji i użytkownika.

- Identyfikator klienta ( `customer-tenant-id` ). Jeśli nie znasz identyfikatora klienta, możesz go znaleźć na pulpicie nawigacyjnym Partner Center [nawigacyjnym](https://partner.microsoft.com/dashboard). Wybierz **pozycję CSP** z menu Partner Center, a następnie pozycję **Klienci.** Wybierz klienta z listy klientów, a następnie wybierz **pozycję Konto**. Na stronie Konto klienta odszukaj identyfikator **Microsoft w** sekcji **Informacje o koncie** klienta. Identyfikator microsoft jest taki sam jak identyfikator klienta ( `customer-tenant-id` ).

- Jeden identyfikator subskrypcji dla subskrypcji początkowej.

### <a name="rest-request"></a>Żądanie REST

#### <a name="request-syntax"></a>Składnia żądania

| Metoda   | Identyfikator URI żądania                                                                                                                         |
|----------|-------------------------------------------------------------------------------------------------------------------------------------|
| **POST**  | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/subscriptions/{subscriptoin-Id}/transitions HTTP/1.1 |


#### <a name="uri-parameter"></a>Parametr URI

Użyj następujących parametrów zapytania, aby wykonać przejście.

| Nazwa                    | Typ     | Wymagane | Opis                                       |
|-------------------------|----------|----------|---------------------------------------------------|
| **identyfikator dzierżawy klienta**  | **guid** | Y        | Identyfikator GUID odpowiadający dzierżawie klienta.             |
| **identyfikator subscriptoin-Id** | **guid** | Y        | Identyfikator GUID odpowiadający początkowej subskrypcji. |

#### <a name="request-headers"></a>Nagłówki żądań

Aby uzyskać więcej informacji, [zobacz Partner Center REST headers (Nagłówki REST).](headers.md)

#### <a name="request-body"></a>Treść żądania

Pełny **zasób Transition** jest wymagany w treści żądania.

#### <a name="request-example"></a>Przykład żądania

```http
GET https://api.partnercenter.microsoft.com/v1/customers/{customerId}/subscriptions/{subscriptionId}/transitions HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 18752a69-1aa1-4ef7-8f9d-eb3681b2d70a
MS-CorrelationId: 81b08ffe-4cf8-49cd-82db-5c2fb0a8e132
X-Locale: en-US

{
    "toCatalogItemId": "CFQ7TTC0KZ59:0001:CFQ7TTC0KZ59",
    "quantity": 5,
    "transitionType": "transition_with_license_transfer",
    "events": []
}
```

### <a name="rest-response"></a>Odpowiedź REST

W przypadku powodzenia ta metoda zwraca zasób Transition z początkowymi zdarzeniami.

#### <a name="response-success-and-error-codes"></a>Kody powodzenia i błędów odpowiedzi

Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie, oraz dodatkowe informacje o debugowaniu. Użyj narzędzia śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry. Aby uzyskać pełną listę, zobacz [Kody błędów](error-codes.md).

#### <a name="response-example"></a>Przykład odpowiedzi

```http
HTTP/1.1 200 OK
Content-Length: 138
Content-Type: application/json
MS-CorrelationId: 81b08ffe-4cf8-49cd-82db-5c2fb0a8e132
MS-RequestId: 18752a69-1aa1-4ef7-8f9d-eb3681b2d70a
Date: Fri, 26 Feb 2021 20:42:26 GMT

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
        }
    ],
    "attributes":
    {
        "objectType": "Transition"
    }
}
```
