---
title: Pobierz bezpośredni stan podpisywania klienta dla umowy Microsoft Customer Agreement.
description: Za pomocą zasobu DirectSignedCustomerAgreementStatus można uzyskać status bezpośredniego podpisywania klienta (bezpośrednie zatwierdzenie) umowy klienta firmy Microsoft.
ms.date: 02/11/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: khpavan
ms.author: sakhanda
ms.openlocfilehash: 3f1deb20a18bc6e7133cac91db528f2d1ad694e2
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/08/2020
ms.locfileid: "97767701"
---
# <a name="get-the-status-of-a-customers-direct-signing-direct-acceptance-of-microsoft-customer-agreement"></a>Uzyskaj status bezpośredniego podpisywania klienta (bezpośrednie zatwierdzenie) umowy klienta firmy Microsoft

**Dotyczy:**

- Centrum partnerskie

Zasób **DirectSignedCustomerAgreementStatus** jest obecnie obsługiwany przez centrum partnerskie tylko w chmurze publicznej firmy Microsoft.

Ten zasób *nie ma zastosowania* do:

- Centrum partnerskie obsługiwane przez firmę 21Vianet
- Centrum partnerskie dla Microsoft Cloud Niemcy
- Centrum partnerskie Microsoft Cloud for US Government

W tym artykule wyjaśniono, jak można pobrać stan bezpośredniej akceptacji umowy klienta firmy Microsoft przez klienta.

## <a name="rest-request"></a>Żądanie REST

Aby pobrać stan bezpośredniej akceptacji umowy klienta firmy Microsoft przez klienta, Utwórz żądanie REST w celu pobrania [DirectSignedCustomerAgreementStatus](./customer-agreement-direct-sign-status-resource.md) dla klienta.

### <a name="request-syntax"></a>Składnia żądania

Użyj następującej składni żądania:

| Metoda | Identyfikator URI żądania                                                                                      |
|--------|--------------------------------------------------------------------------------------------------|
| GET    | [*\{ BASEURL \}*](partner-center-rest-urls.md)/V1/Customers/{Customer-tenant-ID}/directSignedMicrosoftCustomerAgreementStatus http/1.1 |

### <a name="uri-parameters"></a>Parametry identyfikatora URI

Z żądaniem można użyć następujących parametrów URI:

| Nazwa             | Typ | Wymagane | Opis                                                                               |
|------------------|------|----------|-------------------------------------------------------------------------------------------|
| Identyfikator dzierżawy klienta | GUID | Tak | Wartość jest **CustomerTenantId** w formacie GUID, która umożliwia określenie identyfikatora dzierżawy klienta. |

### <a name="request-headers"></a>Nagłówki żądań

Aby uzyskać więcej informacji, zobacz [nagłówki REST Centrum partnerskiego](headers.md).

### <a name="request-body"></a>Treść żądania

Brak.

### <a name="request-example"></a>Przykład żądania

```http
GET https://api.partnercenter.microsoft.com/v1/customers/14876998-c0dc-46e6-9d0c-65a57a6c32ec/directSignedMicrosoftCustomerAgreementStatus HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 94e4e214-6b06-4fb7-96d1-94d559f9b47f
MS-CorrelationId: ab993325-1605-4cf4-bac4-fb584142a31b
```

## <a name="rest-response"></a>Odpowiedź REST

Jeśli to się powiedzie, metoda zwraca [zasób **DirectSignedCustomerAgreementStatus**](./customer-agreement-direct-sign-status-resource.md) w treści odpowiedzi.

Zasób ma właściwość **IsSigned** , która wskazuje stan bezpośredniego podpisywania klienta (zatwierdzenie bezpośrednie).

- Wartość **true** wskazuje, że umowa została podpisana (zaakceptowana) bezpośrednio przez klienta.

- Wartość **false** wskazuje, że umowa *nie* została podpisana (zaakceptowana) bezpośrednio przez klienta.

### <a name="response-success-and-error-codes"></a>Kody sukcesu i błędów odpowiedzi

Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie i dodatkowe informacje debugowania.

Użyj narzędzia do śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry. Aby uzyskać pełną listę, zobacz [kody błędów REST centrum partnera](error-codes.md).

### <a name="response-example"></a>Przykład odpowiedzi

```http
HTTP/1.1 200 OK
Content-Length: 20
Content-Type: application/json
MS-RequestId: 94e4e214-6b06-4fb7-96d1-94d559f9b47f
MS-CorrelationId: ab993325-1605-4cf4-bac4-fb584142a31b

{"isSigned":true}
```
