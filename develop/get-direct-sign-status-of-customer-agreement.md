---
title: Uzyskiwanie stanu bezpośredniego podpisywania klienta dla Umowa z Klientem Microsoft.
description: Możesz użyć zasobu DirectSignedCustomerAgreementStatus, aby uzyskać stan bezpośredniego podpisywania klienta (akceptacja bezpośrednia) Umowa z Klientem Microsoft.
ms.date: 02/11/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: khpavan
ms.author: sakhanda
ms.openlocfilehash: 544965ab05e3956aa5b7b6fa2ef9656ff33990ef9c8d91422797132a814b85f1
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/06/2021
ms.locfileid: "115993354"
---
# <a name="get-the-status-of-a-customers-direct-signing-direct-acceptance-of-microsoft-customer-agreement"></a>Uzyskiwanie stanu bezpośredniego podpisywania klienta (akceptacja bezpośrednia) Umowa z Klientem Microsoft

**Dotyczy:** Partner Center

**Nie dotyczy:** Partner Center obsługiwane przez firmę 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government

Zasób **DirectSignedCustomerAgreementStatus** jest obecnie obsługiwany Partner Center tylko w chmurze publicznej firmy Microsoft.

W tym artykule wyjaśniono, jak można pobrać stan bezpośredniej akceptacji klienta dla Umowa z Klientem Microsoft.

## <a name="prerequisites"></a>Wymagania wstępne

- Poświadczenia zgodnie z opisem w [te Partner Center uwierzytelniania.](partner-center-authentication.md) Ten scenariusz obsługuje uwierzytelnianie tylko przy użyciu poświadczeń aplikacji i użytkownika.

- Identyfikator klienta ( `customer-tenant-id` ). Jeśli nie znasz identyfikatora klienta, możesz go znaleźć na pulpicie nawigacyjnym Partner Center [nawigacyjnym](https://partner.microsoft.com/dashboard). Wybierz **pozycję CSP** z menu Partner Center, a następnie pozycję **Klienci.** Wybierz klienta z listy klientów, a następnie wybierz **pozycję Konto**. Na stronie Konto klienta poszukaj identyfikatora **Microsoft w** sekcji Informacje o **koncie** klienta. Identyfikator microsoft jest taki sam jak identyfikator klienta ( `customer-tenant-id` ).

## <a name="c"></a>C\#

Aby pobrać stan bezpośredniej akceptacji klienta dla klienta Umowa z Klientem Microsoft, wywołaj metodę [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) z identyfikatorem klienta. Następnie użyj właściwości [**Agreements,**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.agreements) aby pobrać [**interfejs ICustomerAgreementCollection.**](/dotnet/api/microsoft.store.partnercenter.agreements.icustomeragreementcollection) Na koniec `GetDirectSignedCustomerAgreementStatus()` wywołaj lub `GetDirectSignedCustomerAgreementStatusAsync()` , aby pobrać stan.

``` csharp
// IAggregatePartner partnerOperations;
// string customerId;
var customerDirectSigningStatus = partnerOperations.Customers.ById(selectedCustomerId).Agreements.GetDirectSignedCustomerAgreementStatus();
```

**Przykład:** [przykładowa aplikacja konsoli](https://github.com/microsoft/Partner-Center-DotNet-Samples). **Project:** SdkSamples, **klasa**: GetDirectSignedCustomerAgreementStatus.cs

## <a name="rest-request"></a>Żądanie REST

Aby pobrać stan bezpośredniej akceptacji klienta dla klienta Umowa z Klientem Microsoft, utwórz żądanie REST w celu pobrania stanu [DirectSignedCustomerAgreementStatus](./customer-agreement-direct-sign-status-resource.md) dla klienta.

### <a name="request-syntax"></a>Składnia żądania

Użyj następującej składni żądania:

| Metoda | Identyfikator URI żądania                                                                                      |
|--------|--------------------------------------------------------------------------------------------------|
| GET    | [*\{ baseURL \}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/directSignedMicrosoftCustomerAgreementStatus HTTP/1.1 |

### <a name="uri-parameters"></a>Parametry URI

W żądaniu możesz użyć następujących parametrów URI:

| Nazwa             | Typ | Wymagane | Opis                                                                               |
|------------------|------|----------|-------------------------------------------------------------------------------------------|
| identyfikator dzierżawy klienta | GUID | Tak | Wartość to identyfikator **CustomerTenantId** w formacie GUID, który umożliwia określenie identyfikatora dzierżawy klienta. |

### <a name="request-headers"></a>Nagłówki żądań

Aby uzyskać więcej informacji, [zobacz Partner Center REST headers (Nagłówki REST).](headers.md)

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

W przypadku powodzenia ta metoda zwraca [ **zasób DirectSignedCustomerAgreementStatus**](./customer-agreement-direct-sign-status-resource.md) w treści odpowiedzi.

Zasób ma właściwość **isSigned,** która wskazuje stan bezpośredniego podpisywania klienta (akceptacja bezpośrednia).

- Wartość true **oznacza,** że umowa została podpisana (zaakceptowana) bezpośrednio przez klienta.

- Wartość false **oznacza,** że umowa nie *została* podpisana (zaakceptowana) bezpośrednio przez klienta.

### <a name="response-success-and-error-codes"></a>Kody powodzenia i błędów odpowiedzi

Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie, oraz dodatkowe informacje o debugowaniu.

Użyj narzędzia śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry. Aby uzyskać pełną listę, zobacz [Partner Center kody błędów REST.](error-codes.md)

### <a name="response-example"></a>Przykład odpowiedzi

```http
HTTP/1.1 200 OK
Content-Length: 20
Content-Type: application/json
MS-RequestId: 94e4e214-6b06-4fb7-96d1-94d559f9b47f
MS-CorrelationId: ab993325-1605-4cf4-bac4-fb584142a31b

{"isSigned":true}
```
