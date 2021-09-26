---
title: Weryfikowanie uprawnień do promocji
description: Sprawdza, czy transakcja klienta kwalifikuje się do danej promocji.
ms.date: 02/23/2021
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: BrentSerbus
ms.author: brserbus
ms.openlocfilehash: ad3346ddca0438c0011e2c6fd03c3ec00b1a1fe3
ms.sourcegitcommit: 7be22de808a10fa2d05577d6497086c8ca3f678a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/24/2021
ms.locfileid: "128715991"
---
# <a name="verify-promotion-eligibility"></a>Weryfikowanie uprawnień do promocji

**Dotyczy**

- Centrum partnerskie

**Odpowiednie role**

- Administrator globalny
- Agent administracyjny

> [!Note] 
> Nowe zmiany handlowe są obecnie dostępne tylko dla partnerów, którzy są częścią nowego Microsoft 365 i dynamics 365 w wersji Technical Preview.

Parters mogą sprawdzić, czy transakcja klienta kwalifikuje się do danej promocji. Ta metoda zwraca *wartość True,* jeśli transakcja klienta kwalifikuje się do danej promocji. Partnerzy mogą zweryfikować uprawnienia przed przesłaniem transakcji, aby upewnić się, że zostanie zastosowana promocja.

## <a name="prerequisites"></a>Wymagania wstępne

- Poświadczenia zgodnie z opisem w te [Partner Center uwierzytelniania.](partner-center-authentication.md) Ten scenariusz obsługuje uwierzytelnianie przy użyciu zarówno poświadczeń aplikacji autonomicznej, jak i aplikacji i użytkownika.

- Uprawnienia obejmują zakupioną dostępność sku produktu, oceniany identyfikator promocji, ilość, czas trwania okresu oraz cykl rozliczeniowy transakcji.

## <a name="rest-request"></a>Żądanie REST

### <a name="request-syntax"></a>Składnia żądania

| Metoda   | Identyfikator URI żądania                                                                                                                         |
|----------|-------------------------------------------------------------------------------------------------------------------------------------|
| **POST**  | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customerId}/promotionEligibilities HTTP/1.1 |

### <a name="uri-parameter"></a>Parametr URI

Użyj następujących parametrów zapytania, aby zwrócić dostępne promocje.

| Nazwa                    | Typ     | Wymagane | Opis                                       |
|-------------------------|----------|----------|---------------------------------------------------|
| **Idklienta**  | **ciąg** | Y        | Wartość jest identyfikatorem customer-tenant-id w formacie identyfikatora GUID, który jest identyfikatorem umożliwiającym określenie klienta.          |

### <a name="request-headers"></a>Nagłówki żądań

Aby uzyskać więcej informacji, [zobacz Partner Center REST headers (Nagłówki REST).](headers.md)

### <a name="request-body"></a>Treść żądania

Treść zawiera kolekcję PromotionEligibilitiesRequestItems. W tej tabeli opisano właściwości obiektu [PromotionEligibilitiesRequestItem.](promotion-resources.md#promotioneligibilitiesrequestitem)

| Właściwość        | Typ             | Wymagane        | Opis                                                                                               |
|-----------------|------------------|-----------------|-----------------------------------------------------------------------------------------------------------|
| catalogItemId   | ciąg           | Tak             | Identyfikator elementu katalogu.                         |
| quantity        | int | Tak        | Liczba licencji lub wystąpień.                 |
| termDuration    | DateTime         | Tak             | Reprezentacja czasu trwania terminu w standardach ISO 8601. Obecnie obsługiwane wartości to P1M (jeden miesiąc), P1Y (jeden rok) i P3Y (trzy lata).   |
| billingCycle    | ciąg | Tak     | Wartość wskazująca typ cyklu rozliczeniowego.   |
| promotionId     | ciąg           | Tak             | Identyfikator elementu poddaną promocji.                       | 

### <a name="request-example"></a>Przykład żądania

```http
POST https://api.partnercenter.microsoft.com/v1/customers/46632f71-f052-4384-8f84-4cdb6c12c2a1/promotionEligibilities HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 18752a69-1aa1-4ef7-8f9d-eb3681b2d70a
MS-CorrelationId: 81b08ffe-4cf8-49cd-82db-5c2fb0a8e132
X-Locale: en-US

{
    "items": [
        {
            "catalogItemId": "CFQ7TTC0KZ59:0001:CFQ7TTC0KZ59",
            "quantity": 1,
            "termDuration": "P1Y",
            "billingCycle": "Monthly",
            "promotionId": " CFQ7TTC0HL8W:0001:CFQ7TTC0K59M"
        }
    ]
}

```

## <a name="rest-response"></a>Odpowiedź REST

W przypadku powodzenia ta metoda zwraca kolekcję wyników uprawnień.

### <a name="response-success-and-error-codes"></a>Kody powodzenia i błędów odpowiedzi

Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie, oraz więcej informacji o debugowaniu. Użyj narzędzia śledzenia sieci, aby odczytać ten kod, typ błędu i inne parametry. Aby uzyskać pełną listę, zobacz [Kody błędów](error-codes.md).

### <a name="response-example"></a>Przykład odpowiedzi

```http
HTTP/1.1 200 OK
Content-Length: 138
Content-Type: application/json
MS-CorrelationId: 81b08ffe-4cf8-49cd-82db-5c2fb0a8e132
MS-RequestId: 18752a69-1aa1-4ef7-8f9d-eb3681b2d70a
Date: Fri, 26 Feb 2021 20:42:26 GMT

{
    "totalCount": 1,
    "items": [
        {
            "catalogItemId": "CFQ7TTC0KZ59:0001:CFQ7TTC0KZ59",
            "quantity": 1,
            "termDuration": "P1Y",
            "billingCycle": "Monthly",
            "eligibilities": [
                {
                    "promotionId": "CFQ9TTC0HH4R:0001:CFQ8HGC0K77G",
                    "isEligible": false,
                    "errors": [
                        {
                            "type": "SeatCount",
                            "minRequiredSeats": 25,
                            "maxRequiredSeats": 500
                        },
                        {
                            "type": "Term",
                            "eligibleTerms": [
                                {
                                    "duration": "P3Y",
                                    "billingCycle": "Monthly"
                                }
                            ]
                        },
                        {
                            "type": "FirstPurchase"
                        }
                    ]
                }
            ],
            "attributes": {
                "objectType": "PromotionEligibilities"
            }
        }
    ],
    "attributes": {
        "objectType": "Collection"
    }
}
```

