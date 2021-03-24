---
title: Pobierz bezpośredni stan podpisywania klienta dla umowy Microsoft Customer Agreement.
description: Za pomocą zasobu DirectSignedCustomerAgreementStatus można uzyskać status bezpośredniego podpisywania klienta (bezpośrednie zatwierdzenie) umowy klienta firmy Microsoft.
ms.date: 02/11/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: khpavan
ms.author: sakhanda
ms.openlocfilehash: 267e3aa63a94c5045977ad566eb5061df3b59882
ms.sourcegitcommit: bbdb5f7c9ddd42c2fc4eaadbb67d61aeeae805ca
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 03/24/2021
ms.locfileid: "105030566"
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

## <a name="prerequisites"></a>Wymagania wstępne

- Poświadczenia zgodnie z opisem w temacie [uwierzytelnianie w centrum partnerskim](partner-center-authentication.md). Ten scenariusz obsługuje tylko uwierzytelnianie przy użyciu aplikacji i poświadczeń użytkownika.

- Identyfikator klienta ( `customer-tenant-id` ). Jeśli nie znasz identyfikatora klienta, możesz go wyszukać na [pulpicie nawigacyjnym](https://partner.microsoft.com/dashboard)Centrum partnerskiego. Wybierz pozycję **dostawca CSP** z menu Centrum partnerskiego, po którym znajdują się **klienci**. Wybierz klienta z listy klient, a następnie wybierz pozycję **konto**. Na stronie konto klienta Znajdź **Identyfikator Microsoft** w sekcji **Informacje o koncie klienta** . Identyfikator Microsoft jest taki sam jak identyfikator klienta ( `customer-tenant-id` ).

## <a name="c"></a>C\#

Aby pobrać stan bezpośredniego akceptacji umowy klienta firmy Microsoft przez klienta, wywołaj metodę [**IAggregatePartner. Customers. ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) z identyfikatorem klienta. Następnie użyj właściwości [**Agreements**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.agreements) , aby pobrać Interfejs [**ICustomerAgreementCollection**](/dotnet/api/microsoft.store.partnercenter.agreements.icustomeragreementcollection) . Na koniec Wywołaj `GetDirectSignedCustomerAgreementStatus()` lub, `GetDirectSignedCustomerAgreementStatusAsync()` Aby pobrać stan.

``` csharp
// IAggregatePartner partnerOperations;
// string customerId;
var customerDirectSigningStatus = partnerOperations.Customers.ById(selectedCustomerId).Agreements.GetDirectSignedCustomerAgreementStatus();
```

**Przykład**: [Przykładowa aplikacja konsolowa](https://github.com/microsoft/Partner-Center-DotNet-Samples). **Projekt**: SdkSamples **Class**: GetDirectSignedCustomerAgreementStatus. cs

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
