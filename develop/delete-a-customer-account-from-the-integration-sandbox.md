---
title: Usuwanie konta klienta z piaskownicy integracji
description: Jak usunąć konto klienta z piaskownicy integracji Testowanie w środowisku produkcyjnym (porada).
ms.date: 06/20/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: b9d9e44ac9c40bd4e3c7e1a9e04253f853dfd96c
ms.sourcegitcommit: ad8082bee01fb1f57da423b417ca1ca9c0df8e45
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/10/2021
ms.locfileid: "111973132"
---
# <a name="delete-a-customer-account-from-the-integration-sandbox"></a>Usuwanie konta klienta z piaskownicy integracji

**Dotyczy:** Partner Center | Partner Center obsługiwana przez firmę 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government

W tym artykule wyjaśniono, jak przerwać relację między partnerem a kontem klienta i odzyskać limit przydziału piaskownicy integracji Testowanie w środowisku produkcyjnym (porada).

> [!IMPORTANT]
> Usunięcie konta klienta spowoduje usunięcie wszystkich zasobów skojarzonych z tą dzierżawą klienta.

## <a name="prerequisites"></a>Wymagania wstępne

- Poświadczenia zgodnie z opisem w te [Partner Center uwierzytelniania.](partner-center-authentication.md) Ten scenariusz obsługuje uwierzytelnianie przy użyciu zarówno poświadczeń aplikacji autonomicznej, jak i aplikacji i użytkownika.

- Identyfikator klienta ( `customer-tenant-id` ). Jeśli nie znasz identyfikatora klienta, możesz go znaleźć na pulpicie nawigacyjnym Partner Center [nawigacyjnym](https://partner.microsoft.com/dashboard). Wybierz **pozycję CSP** z Partner Center menu, a następnie pozycję **Klienci.** Wybierz klienta z listy klientów, a następnie wybierz pozycję **Konto**. Na stronie Konto klienta odszukaj identyfikator **Microsoft w** **sekcji Informacje o koncie** klienta. Identyfikator microsoft jest taki sam jak identyfikator klienta ( `customer-tenant-id` ).

- Wszystkie Azure Reserved Virtual Machine Instances i zamówienia zakupu oprogramowania muszą zostać anulowane przed usunięciem klienta z piaskownicy integracji Porada.

## <a name="c"></a>C\#

Aby usunąć klienta z piaskownicy Porada integracji:

1. Przekaż swoje poświadczenia konta Porada do [**metody CreatePartnerOperations,**](/dotnet/api/microsoft.store.partnercenter.partnerservice.instance) aby uzyskać interfejs [**IPartner**](/dotnet/api/microsoft.store.partnercenter.ipartner) do operacji partnera.

2. Użyj interfejsu operacji partnera, aby pobrać kolekcję uprawnień:

    1. Wywołaj [**metodę Customers.ById()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) z identyfikatorem klienta, aby określić klienta.

    2. Wywołaj **właściwość Entitlements.**

    3. Wywołaj **metodę Get** lub **GetAsync,** aby pobrać [**kolekcję entitlement.**](entitlement-resources.md)

3. Upewnij się, że Azure Reserved Virtual Machine Instances i zamówienia zakupu oprogramowania dla tego klienta zostały anulowane. Dla każdego [**uprawnienia**](entitlement-resources.md) w kolekcji:

    1. Użyj [**uprawnienia . ReferenceOrder.Id**](entitlement-resources.md#referenceorder) uzyskać lokalną kopię odpowiedniego [](order-resources.md#order) zamówienia z kolekcji zamówień klienta.

    2. Ustaw właściwość [**Order.Status**](order-resources.md#order) na wartość "Cancelled".

    3. Użyj metody **Patch(),** aby zaktualizować zamówienie.

4. Anuluj wszystkie zamówienia. Na przykład poniższy przykład kodu używa pętli do sondowania każdego zamówienia do momentu, gdy jego stan to "Cancelled".

    ``` csharp
    // IPartnerCredentials tipAccountCredentials;
    // Customer tenant Id to be deleted.
    // string customerTenantId;

    IPartner tipAccountPartnerOperations = PartnerService.Instance.CreatePartnerOperations(tipAccountCredentials);

    // Get all entitlements whose order must be canceled.
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
        // Check if all the orders were canceled.
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

5. Upewnij się, że wszystkie zamówienia zostały anulowane, wywołując **metodę Delete** dla klienta.

**Przykład:** [aplikacja testowa konsoli](console-test-app.md). **Project:** Partner Center PartnerCenterSDK.FeaturesSamples, **klasa**: DeleteCustomerFromTipAccount.cs

## <a name="rest-request"></a>Żądanie REST

### <a name="request-syntax"></a>Składnia żądania

| Metoda     | Identyfikator URI żądania                                                                            |
|------------|----------------------------------------------------------------------------------------|
| DELETE     | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{identyfikator-dzierżawy-klienta} HTTP/1.1 |

#### <a name="uri-parameter"></a>Parametr URI

Użyj następującego parametru zapytania, aby usunąć klienta.

| Nazwa                   | Typ     | Wymagane | Opis                                                                         |
|------------------------|----------|----------|-------------------------------------------------------------------------------------|
| identyfikator dzierżawy klienta     | GUID     | Y        | Wartość jest identyfikatorem GUID w formacie **customer-tenant-id,** który umożliwia odsprzedawcy filtrowanie wyników dla danego klienta, który należy do odsprzedawcy. |

### <a name="request-headers"></a>Nagłówki żądań

Aby uzyskać więcej informacji, [zobacz Partner Center REST headers (Nagłówki REST).](headers.md)

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

W przypadku powodzenia ta metoda zwraca pustą odpowiedź.

### <a name="response-success-and-error-codes"></a>Kody powodzenia i błędów odpowiedzi

Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie, oraz dodatkowe informacje o debugowaniu. Użyj narzędzia śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry. Aby uzyskać pełną listę, zobacz [Partner Center kodów błędów REST.](error-codes.md)

### <a name="response-example"></a>Przykład odpowiedzi

```http
HTTP/1.1 204 No Content
Content-Length: 0
MS-CorrelationId: 1438ea3d-b515-45c7-9ec1-27ee0cc8e6bd
MS-RequestId: 655890ba-4d2b-4d09-a95f-4ea1348686a5
Date: Wed, 16 Mar 2016 00:43:02 GMT
```
