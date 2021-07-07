---
title: Usuwanie zasad konfiguracji dla określonego klienta
description: Jak usunąć zasady konfiguracji dla określonego klienta i identyfikator zasad.
ms.date: 06/11/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 2d6a7d392bd6af6850eb7716528e6745943bb7bb
ms.sourcegitcommit: ad8082bee01fb1f57da423b417ca1ca9c0df8e45
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/10/2021
ms.locfileid: "111973030"
---
# <a name="delete-a-configuration-policy-for-the-specified-customer"></a>Usuwanie zasad konfiguracji dla określonego klienta

**Dotyczy:** Partner Center | Partner Center for Microsoft Cloud Germany

Jak usunąć zasady konfiguracji dla określonego klienta i identyfikator zasad.

## <a name="prerequisites"></a>Wymagania wstępne

- Poświadczenia zgodnie z opisem w te [Partner Center uwierzytelniania.](partner-center-authentication.md) Ten scenariusz obsługuje uwierzytelnianie przy użyciu zarówno poświadczeń aplikacji autonomicznej, jak i aplikacji i użytkownika.

- Identyfikator klienta ( `customer-tenant-id` ). Jeśli nie znasz identyfikatora klienta, możesz go znaleźć na pulpicie nawigacyjnym Partner Center [nawigacyjnym](https://partner.microsoft.com/dashboard). Wybierz **pozycję CSP** z Partner Center menu, a następnie pozycję **Klienci.** Wybierz klienta z listy klientów, a następnie wybierz pozycję **Konto**. Na stronie Konto klienta odszukaj identyfikator **Microsoft w** **sekcji Informacje o koncie** klienta. Identyfikator microsoft jest taki sam jak identyfikator klienta ( `customer-tenant-id` ).

- Identyfikator zasad.

## <a name="c"></a>C\#

Aby usunąć zasady konfiguracji dla określonego klienta:

1. Wywołaj [**metodę IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) z identyfikatorem klienta, aby pobrać interfejs do operacji na określonym kliencie.

2. Wywołaj [**metodę ConfigurationPolicies.ById z**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.iconfigurationpolicycollection.byid) identyfikatorem zasad, aby pobrać interfejs do operacji zasad konfiguracji dla określonych zasad.

3. Wywołaj [**metodę Delete**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.iconfigurationpolicy.delete) lub [**DeleteAsync,**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.iconfigurationpolicy.deleteasync) aby usunąć zasady konfiguracji.

``` csharp
IAggregatePartner partnerOperations;
string selectedCustomerId;
string selectedPolicyId;

partnerOperations.Customers.ById(selectedCustomerId).ConfigurationPolicies.ById(selectedPolicyId).Delete();
```

**Przykład:** [aplikacja testowa konsoli](console-test-app.md). **Project**: zestaw SDK Centrum partnerskiego Samples Class : DeleteConfigurationPolicy.cs **(Klasa** przykładów zestaw SDK Centrum partnerskiego: DeleteConfigurationPolicy.cs)

## <a name="rest-request"></a>Żądanie REST

### <a name="request-syntax"></a>Składnia żądania

| Metoda     | Identyfikator URI żądania                                                                                          |
|------------|------------------------------------------------------------------------------------------------------|
| **Usunąć** | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{identyfikator-klienta}/policies/{policy-id} HTTP/1.1 |

#### <a name="uri-parameters"></a>Parametry URI

Podczas tworzenia żądania użyj następujących parametrów ścieżki.

| Nazwa        | Typ   | Wymagane | Opis                                                   |
|-------------|--------|----------|---------------------------------------------------------------|
| identyfikator klienta | ciąg | Tak      | Ciąg w formacie identyfikatora GUID, który identyfikuje klienta.         |
| identyfikator zasad   | ciąg | Tak      | Ciąg w formacie identyfikatora GUID, który identyfikuje zasady do usunięcia. |

### <a name="request-headers"></a>Nagłówki żądań

Aby uzyskać więcej informacji, [zobacz Partner Center REST headers (Nagłówki REST).](headers.md)

### <a name="request-body"></a>Treść żądania

Brak

### <a name="request-example"></a>Przykład żądania

```http
DELETE https://api.partnercenter.microsoft.com/v1/customers/47021739-3426-40bf-9601-61b4b6d7c793/policies/56edf752-ee77-4fd8-b7f5-df1f74a3a9ac HTTP/1.1
Authorization: Bearer <token>
MS-RequestId: e88d014d-ab70-41de-90a0-f7fd1797267d
MS-CorrelationId: de894e18-f027-4ac0-8b5a-34f0c222af0c
X-Locale: en-US
Content-Length: 0
Content-Type: application/json
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a>Odpowiedź REST

Jeśli to się powiedzie, odpowiedź zwróci kod stanu 204 Brak zawartości.

### <a name="response-success-and-error-codes"></a>Kody powodzenia i błędów odpowiedzi

Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie, oraz dodatkowe informacje o debugowaniu. Użyj narzędzia śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry. Aby uzyskać pełną listę, zobacz [Partner Center kodów błędów REST.](error-codes.md)

### <a name="response-example"></a>Przykład odpowiedzi

```http
HTTP/1.1 204 No Content
Content-Length: 0
MS-CorrelationId: cee5caf4-c322-4baa-b1d7-e94afb9891a4
MS-RequestId: 76b6f317-1da1-4b61-a6fd-9952439a2c46
MS-CV: YrLe3w6BbUSMt1fi.0
MS-ServerId: 030020344
Date: Tue, 25 Jul 2017 18:10:41 GMT
```
