---
title: Usuwanie konta klienta z piaskownicy integracji
description: Jak usunąć konto klienta z piaskownicy integracji w środowisku produkcyjnym (TIP).
ms.date: 06/20/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: e3a1642c0202c174ddd4f65a6aeda2752def9176
ms.sourcegitcommit: b1ff781b67b1d322820bbcac2c583229201a8c07
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/29/2020
ms.locfileid: "97768157"
---
# <a name="delete-a-customer-account-from-the-integration-sandbox"></a>Usuwanie konta klienta z piaskownicy integracji

**Dotyczy:**

- Centrum partnerskie
- Centrum partnerskie obsługiwane przez firmę 21Vianet
- Centrum partnerskie dla Microsoft Cloud Niemcy
- Centrum partnerskie Microsoft Cloud for US Government

W tym artykule wyjaśniono, jak przerwać relację między partnerem a kontem klienta i odzyskać przydział do testowania w obszarze piaskownicy integracji produkcji (TIP).

> [!IMPORTANT]
> Usunięcie konta klienta spowoduje przeczyszczenie wszystkich zasobów skojarzonych z tą dzierżawą klienta.

## <a name="prerequisites"></a>Wymagania wstępne

- Poświadczenia zgodnie z opisem w temacie [uwierzytelnianie w centrum partnerskim](partner-center-authentication.md). Ten scenariusz obsługuje uwierzytelnianie zarówno w przypadku aplikacji autonomicznych, jak i aplikacji oraz poświadczeń użytkownika.

- Identyfikator klienta ( `customer-tenant-id` ). Jeśli nie znasz identyfikatora klienta, możesz go wyszukać na [pulpicie nawigacyjnym](https://partner.microsoft.com/dashboard)Centrum partnerskiego. Wybierz pozycję **dostawca CSP** z menu Centrum partnerskiego, po którym znajdują się **klienci**. Wybierz klienta z listy klient, a następnie wybierz pozycję **konto**. Na stronie konto klienta Znajdź **Identyfikator Microsoft** w sekcji **Informacje o koncie klienta** . Identyfikator Microsoft jest taki sam jak identyfikator klienta ( `customer-tenant-id` ).

- Wszystkie Azure Reserved Virtual Machine Instances i zamówienia zakupu oprogramowania muszą zostać anulowane przed usunięciem klienta z piaskownicy integracji z poradami.

## <a name="c"></a>C\#

Aby usunąć klienta z piaskownicy integracji z poradami:

1. Przekaż poświadczenia konta TIP do metody [**CreatePartnerOperations**](/dotnet/api/microsoft.store.partnercenter.partnerservice.instance) , aby uzyskać Interfejs [**IPartner**](/dotnet/api/microsoft.store.partnercenter.ipartner) dla operacji partnerskich.

2. Użyj interfejsu operacji partnera do pobrania kolekcji uprawnień:

    1. Wywołaj metodę [**Customers. ById ()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) z identyfikatorem klienta, aby określić klienta.

    2. Wywołaj Właściwość **uprawnienia** .

    3. Wywołaj metodę **Get** lub **GetAsync** , aby pobrać kolekcję [**uprawnień**](entitlement-resources.md) .

3. Upewnij się, że wszystkie Azure Reserved Virtual Machine Instances i zamówienia zakupu oprogramowania dla tego klienta zostały anulowane. Dla każdego [**uprawnienia**](entitlement-resources.md) w kolekcji:

    1. Użyj [**uprawnienia. ReferenceOrder.Id**](entitlement-resources.md#referenceorder) , aby uzyskać lokalną kopię odpowiedniej [kolejności](order-resources.md#order) z kolekcji zamówień klienta.

    2. Ustaw właściwość [**Order. status**](order-resources.md#order) na wartość "anulowana".

    3. Aby zaktualizować kolejność, użyj metody **patch ()** .

4. Anuluj wszystkie zamówienia. Na przykład poniższy kod przykład używa pętli, aby sondować każde zamówienie do momentu, gdy jego stan to "anulowane".

    ``` csharp
    // IPartnerCredentials tipAccountCredentials;
    // Customer tenant Id to be deleted.
    // string customerTenantId;

    IPartner tipAccountPartnerOperations = PartnerService.Instance.CreatePartnerOperations(tipAccountCredentials);

    // Get all entitlements whose order must be cancelled.
    ResourceCollection<Entitlement> entitlements = tipAccountPartnerOperations.Customers.ById(customerTenantId).Entitlements.Get();

    // Cancel all orders
    foreach (var entitlement in entitlements)
    {
        var order = tipAccountPartnerOperations.Customers.ById(customerTenantId).Orders.ById(entitlement.ReferenceOrder.Id).Get();
        order.Status = "Cancelled";
        order = tipAccountPartnerOperations.Customers.ById(customerTenantId).Orders.ById(order.Id).Patch(order);
    }

    // Keep polling until the status of all orders is "Cancelled".
    bool proceed = true;
    do
    {
        // Check if all the orders were cancelled.
        foreach (var entitlement in entitlements)
        {
            var order = tipAccountPartnerOperations.Customers.ById(customerTenantId).Orders.ById(entitlement.ReferenceOrder.Id).Get();
            if (!order.Status.Equals("Cancelled", StringComparison.OrdinalIgnoreCase))
            {
                proceed = false;
            }
        }

        // Wait for a few seconds.
        Thread.Sleep(5000);
    }
    while (proceed == false);

    tipAccountPartnerOperations.Customers.ById(customerTenantId).Delete();
    ```

5. Upewnij się, że wszystkie zamówienia zostały anulowane przez wywołanie metody **delete** dla klienta.

**Przykład**: [aplikacja testowa konsoli](console-test-app.md). **Projekt**: Partner Center PartnerCenterSDK. FeaturesSamples **klasy**: DeleteCustomerFromTipAccount.cs

## <a name="rest-request"></a>Żądanie REST

### <a name="request-syntax"></a>Składnia żądania

| Metoda     | Identyfikator URI żądania                                                                            |
|------------|----------------------------------------------------------------------------------------|
| DELETE     | [*{baseURL}*](partner-center-rest-urls.md)/V1/Customers/{Customer-tenant-ID} http/1.1 |

#### <a name="uri-parameter"></a>Parametr URI

Użyj następującego parametru zapytania, aby usunąć klienta.

| Nazwa                   | Typ     | Wymagane | Opis                                                                         |
|------------------------|----------|----------|-------------------------------------------------------------------------------------|
| Identyfikator dzierżawy klienta     | GUID     | Y        | Wartość jest identyfikatorem GUID z sformatowaną **dzierżawą klienta** , która umożliwia odsprzedawcy filtrowanie wyników dla danego klienta należącego do odsprzedawcy. |

### <a name="request-headers"></a>Nagłówki żądań

Aby uzyskać więcej informacji, zobacz [nagłówki REST Centrum partnerskiego](headers.md).

### <a name="request-body"></a>Treść żądania

Brak.

### <a name="request-example"></a>Przykład żądania

```http
DELETE https://api.partnercenter.microsoft.com/v1/customers/<customer-tenant-id> HTTP/1.1
Accept: application/json
MS-RequestId: 655890ba-4d2b-4d09-a95f-4ea1348686a5
MS-CorrelationId: 1438ea3d-b515-45c7-9ec1-27ee0cc8e6bd
Content-Length: 0
```

## <a name="rest-response"></a>Odpowiedź REST

Jeśli to się powiedzie, ta metoda zwraca pustą odpowiedź.

### <a name="response-success-and-error-codes"></a>Kody sukcesu i błędów odpowiedzi

Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie i dodatkowe informacje debugowania. Użyj narzędzia do śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry. Aby uzyskać pełną listę, zobacz [kody błędów REST centrum partnera](error-codes.md).

### <a name="response-example"></a>Przykład odpowiedzi

```http
HTTP/1.1 204 No Content
Content-Length: 0
MS-CorrelationId: 1438ea3d-b515-45c7-9ec1-27ee0cc8e6bd
MS-RequestId: 655890ba-4d2b-4d09-a95f-4ea1348686a5
Date: Wed, 16 Mar 2016 00:43:02 GMT
```
