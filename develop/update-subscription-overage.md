---
title: Aktualizacje dotyczące nadsyłania aktualizacji dla danego klienta
description: Aktualizacje nadgoręt dla danego klienta.
ms.date: 10/01/2021
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: BrentSerbus
ms.author: brserbus
ms.openlocfilehash: 58590a1882cfe94ddd9779f9e9f766f3e62cffd6
ms.sourcegitcommit: 856c14b6b351697e3b3d33f1fe376adbb80517c5
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/02/2021
ms.locfileid: "129383445"
---
# <a name="update-overage"></a>Aktualizowanie nadgorętowych danych

**Dotyczy**

- Centrum partnerskie

**Odpowiednie role**

- Administrator globalny
- Agent administracyjny

> [!Note] 
> Nowe zmiany w handlu są obecnie dostępne tylko dla partnerów, którzy są częścią nowego Microsoft 365/Dynamics 365 w wersji Technical Preview.

Służy do ustawienia opłat za nadsieć dla danego klienta na subskrypcję zużycia. Może być również używany do usuwania nadwyżu, ustawiając dla niego wartość false. Użycie overage umożliwia klientowi dalsze korzystanie z usług, jeśli nie przekroczy określonych limitów. Opłaty za nadsyłanie opłat za subskrypcję są naliczane zgodnie z ich daniem.

## <a name="prerequisites"></a>Wymagania wstępne

- Poświadczenia zgodnie z opisem w te [Partner Center uwierzytelniania.](partner-center-authentication.md) Ten scenariusz obsługuje uwierzytelnianie przy użyciu zarówno poświadczeń aplikacji autonomicznej, jak i aplikacji i użytkownika.

- Identyfikator klienta ( `customer-tenant-id` ). Jeśli nie znasz identyfikatora klienta, możesz go znaleźć na pulpicie Partner Center [nawigacyjnym](https://partner.microsoft.com/dashboard). Wybierz **pozycję CSP** z menu Partner Center, a następnie pozycję **Klienci.** Wybierz klienta z listy klientów, a następnie wybierz **pozycję Konto**. Na stronie Konto klienta odszukaj identyfikator **Microsoft w** sekcji **Informacje o koncie** klienta. Identyfikator microsoft jest taki sam jak identyfikator klienta ( `customer-tenant-id` ).

- Jeden identyfikator subskrypcji dla subskrypcji, która została przesłoniona.

## <a name="rest-request"></a>Żądanie REST
[PUT] /customers/{customer-tenant-id}/subscriptions/overage
### <a name="request-syntax"></a>Składnia żądania

| Metoda   | Identyfikator URI żądania                                                                                                                         |
|----------|-------------------------------------------------------------------------------------------------------------------------------------|
| **POBIERZ**  | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/subscriptions/overage HTTP/1.1 |

### <a name="uri-parameter"></a>Parametr URI

Użyj następujących parametrów zapytania, aby zwrócić użycie overage klienta.

| Nazwa                    | Typ     | Wymagane | Opis                                       |
|-------------------------|----------|----------|---------------------------------------------------|
| **identyfikator dzierżawy klienta**  | **guid** | Y        | Identyfikator GUID odpowiadający dzierżawie klienta.             |

### <a name="request-headers"></a>Nagłówki żądań

Aby uzyskać więcej informacji, [zobacz Partner Center REST headers (Nagłówki REST).](headers.md)

### <a name="request-body"></a>Treść żądania


| Nazwa                    | Typ     | Opis                                       |
|-------------------------|----------|---------------------------------------------------|
| **azureEntitlementId**  | **guid** | Identyfikator GUID definiujący subskrypcję zużycia dla opłat za zużycie.             |
| **partnerId**  | **guid** | Identyfikator MPN odsprzedawcy pośredniego. Dotyczy tylko modelu dwuwarstwowego (dostawca pośredni).            |

| **overageEnabled**   |  **wartość logiczna** | Określa, czy dla danej subskrypcji zużycia jest włączone nadgorętość.             |


### <a name="request-example"></a>Przykład żądania

```http
GET https://api.partnercenter.microsoft.com/v1/customers/{customer-tenant-id}/subscriptions/overage HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 18752a69-1aa1-4ef7-8f9d-eb3681b2d70a
MS-CorrelationId: 81b08ffe-4cf8-49cd-82db-5c2fb0a8e132
X-Locale: en-US

{
    "azureEntitlementId": "ea1c26b7-8c99-42bb-ba7d-c535831fae8e",
    "partnerId": "5357563",
    "overageEnabled": true
}

```

## <a name="rest-response"></a>Odpowiedź REST

W przypadku powodzenia ta metoda zwraca przesłony dla klienta.

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
    "azureEntitlementId": "ea1c26b7-8c99-42bb-ba7d-c535831fae8e",
    "partnerId": "5357563",
    "type": "PhoneServices",
    "overageEnabled": true,
    "links": {
        "overage": {
            "uri": "/customers/f62cf10b-8f76-4fc4-9774-c5291f8faf86/subscriptions/overage",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "Overage"
    }
}
```
