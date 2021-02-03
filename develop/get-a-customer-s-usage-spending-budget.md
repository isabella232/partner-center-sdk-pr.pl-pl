---
title: Pobierz budżet wydatków użycia klienta
description: Możesz użyć budżetu wydatków (obiektu SpendingBudget), aby zaktualizować Podsumowanie użycia klienta (zasób CustomerUsageSummary).
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 8be9ceaab6b7546de8eacba1e52e8766719e5125
ms.sourcegitcommit: 58801b7a09c19ce57617ec4181a008a673b725f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/22/2020
ms.locfileid: "97768105"
---
# <a name="get-a-customers-usage-spending-budget"></a>Pobierz budżet wydatków użycia klienta

**Dotyczy:**

- Centrum partnerskie
- Centrum partnerskie dla Microsoft Cloud Niemcy
- Centrum partnerskie Microsoft Cloud for US Government

Budżet wydatków (obiekt **SpendingBudget** ) można zaktualizować w [podsumowaniu użytkowania klienta (zasób **CustomerUsageSummary** )](customer-usage-resources.md#customerusagesummary).

## <a name="prerequisites"></a>Wymagania wstępne

- Poświadczenia zgodnie z opisem w temacie [uwierzytelnianie w centrum partnerskim](partner-center-authentication.md). Ten scenariusz obsługuje uwierzytelnianie zarówno w przypadku aplikacji autonomicznych, jak i aplikacji oraz poświadczeń użytkownika.

- Identyfikator klienta ( `customer-tenant-id` ). Jeśli nie znasz identyfikatora klienta, możesz go wyszukać na [pulpicie nawigacyjnym](https://partner.microsoft.com/dashboard)Centrum partnerskiego. Wybierz pozycję **dostawca CSP** z menu Centrum partnerskiego, po którym znajdują się **klienci**. Wybierz klienta z listy klient, a następnie wybierz pozycję **konto**. Na stronie konto klienta Znajdź **Identyfikator Microsoft** w sekcji **Informacje o koncie klienta** . Identyfikator Microsoft jest taki sam jak identyfikator klienta ( `customer-tenant-id` ).

## <a name="c"></a>C\#

Aby zaktualizować budżet wydatków użycia klienta:

1. Utwórz nowy obiekt [**SpendingBudget**](/dotnet/api/microsoft.store.partnercenter.models.usage.spendingbudget) ze zaktualizowaną kwotą.

2. Użyj kolekcji [**IAggregatePartner. Customers**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection) , aby wywołać metodę [**ById ()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) przy użyciu identyfikatora określonego klienta.

3. Wywołaj metodę [**Get**](/dotnet/api/microsoft.store.partnercenter.subscribedskus.icustomersubscribedskucollection.get) lub [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.subscribedskus.icustomersubscribedskucollection.getasync) , aby uzyskać budżet użycia klienta.

``` csharp
// IAggregatePartner partnerOperations;
// string selectedCustomerId;

// Create a new spending budget with the udpated amount.
var newUsageBudget = new SpendingBudget()
{
    Amount = 100
};

// Update the customer's usage budget.
var usageBudget = partnerOperations.Customers.ById(selectedCustomerId).UsageBudget.Get();
```

## <a name="rest-request"></a>Żądanie REST

### <a name="request-syntax"></a>Składnia żądania

| Metoda    | Identyfikator URI żądania                                                                                             |
|-----------|---------------------------------------------------------------------------------------------------------|
| **Pobierz** | [*{baseURL}*](partner-center-rest-urls.md)/V1/Customers/{Customer-tenant-ID}/usagebudget http/1.1 |

### <a name="uri-parameter"></a>Parametr URI

Użyj następującego parametru zapytania, aby zaktualizować profil rozliczeń.

| Nazwa                   | Typ     | Wymagane | Opis                                                                                                                                            |
|------------------------|----------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Identyfikator dzierżawy klienta** | **guid** | Y        | Wartość jest identyfikatorem GUID z sformatowaną **dzierżawą klienta** , która umożliwia odsprzedawcy filtrowanie wyników dla danego klienta należącego do odsprzedawcy. |

### <a name="request-headers"></a>Nagłówki żądań

Aby uzyskać więcej informacji, zobacz [nagłówki REST Centrum partnerskiego](headers.md).

### <a name="request-body"></a>Treść żądania

Pełny zasób.

### <a name="request-example"></a>Przykład żądania

```http
GET https://api.partnercenter.microsoft.com/v1/customers/<customer-tenant-id>/usagebudget HTTP/1.1
Authorization: Bearer <token>
Accept: application/json, text/plain, */*
MS-RequestId: 312b044d-dc41-4b37-c2d5-7d27322d9654
MS-CorrelationId: 7cb67bb7-4750-403d-cc2e-6bc44c52d52c
Content-Type: application/json;charset=utf-8
X-Locale: "en-US"
```

## <a name="rest-response"></a>Odpowiedź REST

Jeśli to się powiedzie, ta metoda zwraca budżet wydatków użytkownika ze zaktualizowaną kwotą.

### <a name="response-success-and-error-codes"></a>Kody sukcesu i błędów odpowiedzi

Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie i dodatkowe informacje debugowania. Użyj narzędzia do śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry. Aby uzyskać pełną listę, zobacz [kody błędów](error-codes.md).

### <a name="response-example"></a>Przykład odpowiedzi

```http
HTTP/1.1 200 OK
Content-Length: 12014
Content-Type: application/json
MS-CorrelationId: 7cb67bb7-4750-403d-cc2e-6bc44c52d52c
MS-RequestId: be82a8ba-4a53-49f7-8313-b033c058687e
Date: Tue, 17 Sep 2019 20:31:45 GMT

{
    {
        "amount": 100,
        "usageSpendingBudget": 100,
        "attributes":{
            "objectType":"SpendingBudget"
        }
    },
    "links":{
        "self":{
            "uri":"/v1/customers/<customer-tenant-id>/usagebudget",
            "method":"GET",
            "headers":[]
        }
    }
}
```
