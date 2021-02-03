---
title: Wycofywanie transferu
description: Jak wycofać utworzony transfer subskrypcji dla klienta.
ms.date: 04/10/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: a9e1e2a33d21fc1338a36b8ac96b528e70b61c86
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/08/2020
ms.locfileid: "97767677"
---
# <a name="withdraw-a-transfer"></a>Wycofywanie transferu

**Dotyczy:**

- Centrum partnerskie

## <a name="prerequisites"></a>Wymagania wstępne

- Poświadczenia zgodnie z opisem w temacie [uwierzytelnianie w centrum partnerskim](partner-center-authentication.md). Ten scenariusz obsługuje uwierzytelnianie zarówno w przypadku aplikacji autonomicznych, jak i aplikacji oraz poświadczeń użytkownika.

- Identyfikator klienta ( `customer-tenant-id` ). Jeśli nie znasz identyfikatora klienta, możesz go wyszukać na [pulpicie nawigacyjnym](https://partner.microsoft.com/dashboard)Centrum partnerskiego. Wybierz pozycję **dostawca CSP** z menu Centrum partnerskiego, po którym znajdują się **klienci**. Wybierz klienta z listy klient, a następnie wybierz pozycję **konto**. Na stronie konto klienta Znajdź **Identyfikator Microsoft** w sekcji **Informacje o koncie klienta** . Identyfikator Microsoft jest taki sam jak identyfikator klienta ( `customer-tenant-id` ).

- Identyfikator transferu dla istniejącego transferu.

## <a name="rest-request"></a>Żądanie REST

### <a name="request-syntax"></a>Składnia żądania

| Metoda    | Identyfikator URI żądania                                                                                                 |
|-----------|-------------------------------------------------------------------------------------------------------------|
| **USUNIĘTY**| [*{baseURL}*](partner-center-rest-urls.md)/V1/Customers/{Customer-ID}/Transfers/{transfer-ID} http/1.1      |

### <a name="uri-parameter"></a>Parametr URI

Użyj następującego parametru ścieżki, aby zidentyfikować klienta.

| Nazwa            | Typ     | Wymagane | Opis                                                            |
|-----------------|----------|----------|------------------------------------------------------------------------|
| **Identyfikator klienta** | ciąg   | Tak      | Identyfikator GUID sformatowany przez klienta, który identyfikuje klienta.             |
| **Identyfikator transferu** | ciąg   | Tak      | Identyfikator transferu w formacie GUID, który identyfikuje transfer.             |

### <a name="request-headers"></a>Nagłówki żądań

Aby uzyskać więcej informacji, zobacz [nagłówki REST Centrum partnerskiego](headers.md).

### <a name="request-example"></a>Przykład żądania

```http
DELETE /v1/customers/d6bf25b7-e0a8-4f2d-a31b-97b55cfc774d/transfers/67c5b05b-09b5-47ba-9047-5056fe2afa4f HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: cdf6e25c-7b32-4cc3-d8bc-53e0b37eebd8
MS-CorrelationId: 9041d76d-8915-43a8-8e82-00ca46a1a73d
Connection: keep-alive
```

## <a name="rest-response"></a>Odpowiedź REST

Jeśli to się powiedzie, ta metoda nie zwróci zawartości (204).

### <a name="response-success-and-error-codes"></a>Kody sukcesu i błędów odpowiedzi

Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie i dodatkowe informacje debugowania. Użyj narzędzia do śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry. Aby uzyskać pełną listę, zobacz [kody błędów](error-codes.md).

### <a name="response-example"></a>Przykład odpowiedzi

```http
HTTP/1.1 204 No Content
Content-Length: 0
MS-CorrelationId: 9041d76d-8915-43a8-8e82-00ca46a1a73d
MS-RequestId: cdf6e25c-7b32-4cc3-d8bc-53e0b37eebd8
Date: Tue, 24 Mar 2020 23:44:06 GMT
```
