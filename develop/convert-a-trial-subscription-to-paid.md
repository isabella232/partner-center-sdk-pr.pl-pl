---
title: Konwertowanie wersji próbnej subskrypcji na płatną
description: Dowiedz się, jak używać interfejsów API usługi Partner Center, aby przekonwertować subskrypcję wersji próbnej na płatną.
ms.date: 05/23/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 59dcf6caf21d407b2fba4cc8438bc435fda9dc77
ms.sourcegitcommit: a25d4951f25502cdf90cfb974022c5e452205f42
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/04/2020
ms.locfileid: "97768585"
---
# <a name="convert-a-trial-subscription-to-paid-using-partner-center-apis"></a>Konwertuj subskrypcję wersji próbnej na płatną przy użyciu interfejsów API Centrum partnerskiego

**Dotyczy:**

- Centrum partnerskie

Możesz przekonwertować subskrypcję wersji próbnej na płatną.

## <a name="prerequisites"></a>Wymagania wstępne

- Poświadczenia zgodnie z opisem w temacie [uwierzytelnianie w centrum partnerskim](partner-center-authentication.md). Ten scenariusz obsługuje tylko uwierzytelnianie przy użyciu aplikacji i poświadczeń użytkownika.

- Identyfikator klienta ( `customer-tenant-id` ). Jeśli nie znasz identyfikatora klienta, możesz go wyszukać na [pulpicie nawigacyjnym](https://partner.microsoft.com/dashboard)Centrum partnerskiego. Wybierz pozycję **dostawca CSP** z menu Centrum partnerskiego, po którym znajdują się **klienci**. Wybierz klienta z listy klient, a następnie wybierz pozycję **konto**. Na stronie konto klienta Znajdź **Identyfikator Microsoft** w sekcji **Informacje o koncie klienta** . Identyfikator Microsoft jest taki sam jak identyfikator klienta ( `customer-tenant-id` ).

- Identyfikator subskrypcji aktywnej subskrypcji próbnej.

- Dostępna oferta konwersji.

## <a name="convert-a-trial-subscription-to-paid-through-code"></a>Konwertuj subskrypcję wersji próbnej na płatną za pomocą kodu

Aby przekonwertować subskrypcję próbną na płatną, należy najpierw uzyskać kolekcję dostępnych konwersji. Następnie musisz wybrać ofertę konwersji, którą chcesz zakupić.

Oferty konwersji określają liczbę domyślną dla tej samej liczby licencji co subskrypcja wersji próbnej. Tę ilość można zmienić, ustawiając właściwość [**ilość**](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.conversion.quantity) na liczbę licencji, które chcesz zakupić.

> [!NOTE]
> Niezależnie od liczby zakupionych licencji Identyfikator subskrypcji wersji próbnej jest ponownie używany w przypadku zakupionych licencji. W związku z tym, okres próbny znika i jest zastępowany przez zakup.

Wykonaj następujące kroki, aby przekonwertować subskrypcję próbną za pomocą kodu:

1. Uzyskaj interfejs do dostępnych operacji subskrypcji. Należy zidentyfikować klienta i określić identyfikator subskrypcji wersji próbnej subskrypcji.

    ``` csharp
    var subscriptionOperations = partnerOperations.Customers.ById(customerId).Subscriptions.ById(subscriptionId);
    ```

2. Pobierz kolekcję dostępnych ofert konwersji. Aby uzyskać więcej informacji i szczegóły dotyczące żądania/odpowiedzi dla tej metody, zobacz [Pobieranie listy ofert konwersji wersji próbnej](get-a-list-of-trial-conversion-offers.md).

    ``` csharp
    var conversions = subscriptionOperations.Conversions.Get();
    ```

3. Wybierz ofertę konwersji. Poniższy kod wybiera pierwszą ofertę konwersji w kolekcji.

    ``` csharp
    var selectedConversion = conversions.Items.ToList()[0];
    ```

4. Opcjonalnie możesz określić liczbę licencji do zakupu. Wartość domyślna to liczba licencji w subskrypcji wersji próbnej.

    ``` csharp
    selectedConversion.Quantity = 10;
    ```

5. Wywołaj metodę [**Create**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionupgradecollection.create) lub [**onasync**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionupgradecollection.createasync) , aby przekonwertować subskrypcję wersji próbnej na płatne.

    ``` csharp
    var convertResult = subscriptionOperations.Conversions.Create(selectedConversion);
    ```

## <a name="c"></a>C\#

Aby przekonwertować subskrypcję próbną na jedną płatną:

1. Użyj metody [**IAggregatePartner. Customers. ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) z identyfikatorem klienta, aby zidentyfikować klienta.

2. Uzyskaj interfejs do operacji subskrybowania, wywołując metodę [**Subscription. ById**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.byid) z identyfikatorem subskrypcji wersji próbnej. Zapisz odwołanie do interfejsu operacji subskrypcji w zmiennej lokalnej.

3. Użyj właściwości [**konwersje**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscription.conversions) , aby uzyskać interfejs do dostępnych operacji dla konwersji, a następnie wywołać metodę [**Get**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionconversioncollection.get) lub [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionconversioncollection.getasync) w celu pobrania kolekcji dostępnych ofert [**konwersji**](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.conversion) . Musisz wybrać jeden z nich. Poniższy przykład jest wartością domyślną dla pierwszej dostępnej konwersji.

4. Użyj odwołania do interfejsu operacji subskrypcji zapisanego w zmiennej lokalnej i właściwości [**konwersje**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscription.conversions) , aby uzyskać interfejs do dostępnych operacji na konwersji.

5. Przekaż wybrany obiekt oferty konwersji do metody [**Create**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionupgradecollection.create) lub [**IsAsync**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionupgradecollection.createasync) w celu próby konwersji wersji próbnej.

### <a name="c-example"></a>\#Przykład C

``` csharp
// IAggregatePartner partnerOperations;
// string customerId;
// string subscriptionId;

// Get subscription operations for the trial subscription.
var subscriptionOperations = partnerOperations.Customers.ById(customerId).Subscriptions.ById(subscriptionId);

// Get the available conversions.
var conversions = subscriptionOperations.Conversions.Get();

// If there are no conversions available, we&#39;re done.
// Otherwise, convert the trial to the first available conversion offer.
if (conversions.TotalCount <= 0)
{
    System.Console.WriteLine("This subscription has no conversions");
}
else
{
    // Default to the first conversion.
    var selectedConversion = conversions.Items.ToList()[0];

    // Convert the trial and return the result.
    var convertResult = subscriptionOperations.Conversions.Create(selectedConversion);
}
```

## <a name="rest-request"></a>Żądanie REST

### <a name="request-syntax"></a>Składnia żądania

| Metoda   | Identyfikator URI żądania                                                                                                                 |
|----------|-----------------------------------------------------------------------------------------------------------------------------|
| **POUBOJOWEGO** | [*{baseURL}*](partner-center-rest-urls.md)/V1/Customers/{Customer-ID}/subscriptions/{Subscription-ID}/conversions http/1.1 |

### <a name="uri-parameter"></a>Parametr URI

Użyj następujących parametrów ścieżki, aby zidentyfikować klienta i subskrypcję wersji próbnej.

| Nazwa            | Typ   | Wymagane | Opis                                                     |
|-----------------|--------|----------|-----------------------------------------------------------------|
| Identyfikator klienta     | ciąg | Tak      | Ciąg w formacie GUID, który identyfikuje klienta.           |
| Identyfikator subskrypcji | ciąg | Tak      | Ciąg w formacie GUID, który identyfikuje subskrypcję wersji próbnej. |

### <a name="request-headers"></a>Nagłówki żądań

Aby uzyskać więcej informacji, zobacz [nagłówki REST Centrum partnerskiego](headers.md).

### <a name="request-body"></a>Treść żądania

W treści żądania musi znajdować się wypełniony zawarty zasób [konwersji](conversions-resources.md#conversion) .

### <a name="request-example"></a>Przykład żądania

```http
POST https://api.partnercenter.microsoft.com/v1/customers/0c39d6d5-c70d-4c55-bc02-f620844f3fd1/subscriptions/488745B5-2086-4912-802C-6ABB9F7C3638/conversions HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: bd0cde7f-ba87-4010-8a73-1190b641f2a4
MS-CorrelationId: 8daa6d54-72ab-4d6b-9c7d-9266d3734a47
X-Locale: en-US
Content-Type: application/json
Host: api.partnercenter.microsoft.com
Content-Length: 234
Expect: 100-continue

{
    "OfferId": "C0BD2E08-11AC-4836-BDC7-3712E744922F",
    "TargetOfferId": "031C9E47-4802-4248-838E-778FB1D2CC05",
    "OrderId": "D51A052E-043C-4A2A-AA37-2BB938CEF6C1",
    "Quantity": 25,
    "BillingCycle": "monthly",
    "Attributes": {
        "ObjectType": "Conversion"
    }
}
```

## <a name="rest-response"></a>Odpowiedź REST

Jeśli to się powiedzie, treść odpowiedzi zawiera zasób [ConversionResult](conversions-resources.md#conversionresult) .

#### <a name="response-success-and-error-codes"></a>Kody sukcesu i błędów odpowiedzi

Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie i dodatkowe informacje debugowania. Użyj narzędzia do śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry. Aby uzyskać pełną listę, zobacz [kody błędów Centrum partnerskiego](error-codes.md).

#### <a name="response-example"></a>Przykład odpowiedzi

```http
HTTP/1.1 200 OK
Content-Length: 211
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 8daa6d54-72ab-4d6b-9c7d-9266d3734a47
MS-RequestId: bd0cde7f-ba87-4010-8a73-1190b641f2a4
MS-CV: kW4GzmhvHEqCq1ls.0
MS-ServerId: 030020643
Date: Thu, 15 Jun 2017 23:10:40 GMT

 {
    "subscriptionId": "488745B5-2086-4912-802C-6ABB9F7C3638",
    "offerId": "C0BD2E08-11AC-4836-BDC7-3712E744922F",
    "targetOfferId": "031C9E47-4802-4248-838E-778FB1D2CC05",
    "attributes": {
        "objectType": "ConversionResult"
    }
}
```
