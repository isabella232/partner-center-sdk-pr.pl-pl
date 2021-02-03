---
title: Pobierz szczegóły transferu według identyfikatora
description: Jak uzyskać szczegółowe informacje dotyczące transferu subskrypcji dla klienta.
ms.date: 04/10/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: c39e9483f1e51469981b0d6fa2541a6372ff2dac
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/08/2020
ms.locfileid: "97767814"
---
# <a name="get-transfer-details-by-id"></a>Pobierz szczegóły transferu według identyfikatora

**Dotyczy:**

- Centrum partnerskie

## <a name="prerequisites"></a>Wymagania wstępne

- Poświadczenia zgodnie z opisem w temacie [uwierzytelnianie w centrum partnerskim](partner-center-authentication.md). Ten scenariusz obsługuje uwierzytelnianie zarówno w przypadku aplikacji autonomicznych, jak i aplikacji oraz poświadczeń użytkownika.

- Identyfikator klienta ( `customer-tenant-id` ). Jeśli nie znasz identyfikatora klienta, możesz go wyszukać na [pulpicie nawigacyjnym](https://partner.microsoft.com/dashboard)Centrum partnerskiego. Wybierz pozycję **dostawca CSP** z menu Centrum partnerskiego, po którym znajdują się **klienci**. Wybierz klienta z listy klient, a następnie wybierz pozycję **konto**. Na stronie konto klienta Znajdź **Identyfikator Microsoft** w sekcji **Informacje o koncie klienta** . Identyfikator Microsoft jest taki sam jak identyfikator klienta ( `customer-tenant-id` ).

- Identyfikator transferu dla istniejącego transferu.

## <a name="rest-request"></a>Żądanie REST

### <a name="request-syntax"></a>Składnia żądania

| Metoda   | Identyfikator URI żądania                                                                                                 |
|----------|-------------------------------------------------------------------------------------------------------------|
| **Pobierz** | [*{baseURL}*](partner-center-rest-urls.md)/V1/Customers/{Customer-ID}/Transfers/{transfer-ID} http/1.1                    |

### <a name="uri-parameter"></a>Parametr URI

Użyj następującego parametru ścieżki, aby zidentyfikować klienta i określić transfer, który ma zostać zaakceptowany.

| Nazwa            | Typ     | Wymagane | Opis                                                            |
|-----------------|----------|----------|------------------------------------------------------------------------|
| **Identyfikator klienta** | ciąg   | Tak      | Identyfikator GUID sformatowany przez klienta, który identyfikuje klienta.             |
| **Identyfikator transferu** | ciąg   | Tak      | Identyfikator transferu w formacie GUID, który identyfikuje transfer.             |

### <a name="request-headers"></a>Nagłówki żądań

Aby uzyskać więcej informacji, zobacz [nagłówki REST Centrum partnerskiego](headers.md).

### <a name="request-example"></a>Przykład żądania

```http
GET /v1/customers/b67f0b00-f9e8-4c57-bcb5-0b8b95c6ccf0/transfers/46e8ed67-8adf-4f65-b3d8-d31318080556 HTTP/1.1
Authorization: Bearer <token>
Connection: keep-alive
MS-RequestId: 0d61b5ce-b396-4f5e-a50b-e8779d0d23cc
MS-CorrelationId: 68eacc61-971c-43b0-c06f-2622bf79b090
Accept: application/json
```

## <a name="rest-response"></a>Odpowiedź REST

Jeśli to się powiedzie, ta metoda zwraca wypełniony zasób [TransferEntity](transfer-entity-resources.md) w treści odpowiedzi.

### <a name="response-success-and-error-codes"></a>Kody sukcesu i błędów odpowiedzi

Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie i dodatkowe informacje debugowania. Użyj narzędzia do śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry. Aby uzyskać pełną listę, zobacz [kody błędów](error-codes.md).

### <a name="response-example"></a>Przykład odpowiedzi

```http
HTTP/1.1 200 OK
Content-Length: 1501
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 68eacc61-971c-43b0-c06f-2622bf79b090
MS-RequestId: 0d61b5ce-b396-4f5e-a50b-e8779d0d23cc
X-Locale: en-US
Date: Fri, 27 Mar 2020 18:25:25 GMT

{
  "id": "46e8ed67-8adf-4f65-b3d8-d31318080556",
  "status": "Active",
  "createdTime": "2020-03-27T18:22:33.2875302Z",
  "lastModifiedTime": "2020-03-27T18:22:33Z",
  "customerTenantId": "b67f0b00-f9e8-4c57-bcb5-0b8b95c6ccf0",
  "partnertenantid": "3a9a35ce-d5be-4814-ab58-4451c36fe157",
  "sourcePartnerName": "Test_Test_09092019GBL",
  "sourcePartnerTenantId": "7c8db11f-1e5e-4472-8386-f0b627d1f3e1",
  "targetPartnerName": "Test_Test_09032019GBL",
  "targetPartnerTenantId": "3a9a35ce-d5be-4814-ab58-4451c36fe157",
  "lastModifiedUser": "edc0524d-2e42-4619-af7e-349c015cfdfd",
  "lineItems": [
    {
      "id": 0,
      "subscriptionId": "75B71186-73C3-45B4-A403-281C0D7EB032",
      "offerId": "F72752C8-3E37-4C9B-A1A0-69E8442068DC",
      "billingCycle": "annual",
      "friendlyName": "Dynamics 365 Business Central Team Member",
      "quantity": 1,
      "partnerIdOnRecord": "5139005",
      "addonItems": [

      ]
    },
    {
      "id": 1,
      "subscriptionId": "1FB4CB0A-EB79-4300-9E87-7D486054888A",
      "offerId": "88F9EB8A-0636-45E8-A601-553E0A48AA9E",
      "billingCycle": "annual",
      "friendlyName": "Dynamics 365 Business Central External Accountant",
      "quantity": 1,
      "partnerIdOnRecord": "5139005",
      "addonItems": [

      ]
    },
    {
      "id": 2,
      "subscriptionId": "08AB3010-B647-402E-8955-B6C0FB364D8F",
      "offerId": "4D8F3B90-29B3-4E7B-B37C-4A435DDEF1D9",
      "billingCycle": "annual",
      "friendlyName": "Common Area Phone",
      "quantity": 1,
      "partnerIdOnRecord": "5139005",
      "addonItems": [

      ]
    }
  ],
  "links": {
    "self": {
      "uri": "/customers/b67f0b00-f9e8-4c57-bcb5-0b8b95c6ccf0/transfers/46e8ed67-8adf-4f65-b3d8-d31318080556",
      "method": "GET",
      "headers": [

      ]
    }
  },
  "attributes": {
    "objectType": "TransferEntity"
  }
}

```
