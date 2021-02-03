---
title: Pobieranie uprawnień klienta do przeniesienia subskrypcji
description: Jak uzyskać kolekcję subskrypcji klienta, które są uprawnione/ineligibile do przeniesienia.
ms.date: 04/10/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: khpavan
ms.author: sakhanda
ms.openlocfilehash: 43086a32fa0dbbdecf65aac167c687f26fc4c2c6
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/08/2020
ms.locfileid: "97767702"
---
# <a name="get-a-customers-subscriptions-transfer-eligibility"></a>Pobieranie uprawnień klienta do przeniesienia subskrypcji

**Dotyczy**

- Centrum partnerskie

Jak uzyskać kolekcję subskrypcji klienta uprawniających/niekwalifikujących się do przeniesienia.

## <a name="prerequisites"></a>Wymagania wstępne

- Poświadczenia zgodnie z opisem w temacie [uwierzytelnianie w centrum partnerskim](partner-center-authentication.md). Ten scenariusz obsługuje uwierzytelnianie zarówno w przypadku aplikacji autonomicznych, jak i aplikacji oraz poświadczeń użytkownika.

- Identyfikator klienta ( `customer-tenant-id` ). Jeśli nie znasz identyfikatora klienta, możesz go wyszukać na [pulpicie nawigacyjnym](https://partner.microsoft.com/dashboard)Centrum partnerskiego. Wybierz pozycję **dostawca CSP** z menu Centrum partnerskiego, po którym znajdują się **klienci**. Wybierz klienta z listy klient, a następnie wybierz pozycję **konto**. Na stronie konto klienta Znajdź **Identyfikator Microsoft** w sekcji **Informacje o koncie klienta** . Identyfikator Microsoft jest taki sam jak identyfikator klienta ( `customer-tenant-id` ).

## <a name="rest-request"></a>Żądanie REST

### <a name="request-syntax"></a>Składnia żądania

| Metoda  | Identyfikator URI żądania                                                                                          |
|---------|------------------------------------------------------------------------------------------------------|
| **Pobierz** | [*{baseURL}*](partner-center-rest-urls.md)/V1/Customers/{Customer-tenant-ID}/transferseligibility? typ transferu = {transfer-Type} http/1.1 |

### <a name="uri-parameter"></a>Parametr URI

Ta tabela zawiera listę wymaganych parametrów zapytania w celu uzyskania wszystkich subskrypcji.

| Nazwa               | Typ   | Wymagane | Opis                                           |
|--------------------|--------|----------|-------------------------------------------------------|
| Identyfikator dzierżawy klienta | ciąg | Tak      | Ciąg sformatowany przez identyfikator GUID, który identyfikuje klienta. |
| Typ transferu      | ciąg | Tak      | Typ transferu, który jest przeznaczony.                |

### <a name="request-headers"></a>Nagłówki żądań

Aby uzyskać więcej informacji, zobacz [nagłówki REST Centrum partnerskiego](headers.md).

### <a name="request-body"></a>Treść żądania

Brak.

### <a name="request-example"></a>Przykład żądania

```http
GET /v1/customers/823c6c3f-9259-4d51-bae2-5dd06743177f/transferseligibility?transferType=directtoindirect HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 202b5e9a-ae82-4ab9-8a0a-f4e9e04eb14d
MS-CorrelationId: cd589c16-dc94-49ad-e529-125c258573d6
Connection: Keep-Alive
```

## <a name="rest-response"></a>Odpowiedź REST

Jeśli to się powiedzie, ta metoda zwraca kolekcję zasobów [TransferEligibility](transfer-eligibility-resources.md) w treści odpowiedzi.

### <a name="response-success-and-error-codes"></a>Kody sukcesu i błędów odpowiedzi

Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie i dodatkowe informacje debugowania. Użyj narzędzia do śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry. Aby uzyskać pełną listę, zobacz [kody błędów REST centrum partnera](error-codes.md).

### <a name="response-example"></a>Przykład odpowiedzi

```http
HTTP/1.1 200 OK
Content-Length: 73754
Content-Type: application/json
MS-CorrelationId: cd589c16-dc94-49ad-e529-125c258573d6
MS-RequestId: 202b5e9a-ae82-4ab9-8a0a-f4e9e04eb14d
Date: Tue, 24 Mar 2020 23:43:25 GMT

[
  {
    "id": "548FA265-5F40-4765-9A6B-47826F72A4BF",
    "isEligible": false,
    "reason": "Subscription: 548FA265-5F40-4765-9A6B-47826F72A4BF is in state: Deleted"
  },
  {
    "id": "E2A3AEB3-70A7-42E3-930C-7519EEDDC45A",
    "isEligible": false,
    "reason": "Subscription: E2A3AEB3-70A7-42E3-930C-7519EEDDC45A is in state: Suspended"
  },
  {
    "id": "4B600A9A-DF56-4564-A75A-6CC6D2D0C9F9",
    "isEligible": false,
    "reason": "subscription is already part of another transfer request id : 31a06eac-c527-458a-a6b4-0de197a45996"
  },
  {
    "id": "D3350F46-AA29-4F6F-95A0-E3011988915C",
    "isEligible": true
  }
  {
    "id": "E82B2F4A-736A-4E2B-955C-C1A4C56C0171",
    "isEligible": true
  }
]
```
