---
title: Konwertowanie wersji próbnej subskrypcji na płatną
description: Dowiedz się, jak za pomocą Partner Center API przekonwertować subskrypcję wersji próbnej na płatną.
ms.date: 05/23/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: a805264315e35c7576248630396da1e34a66cc55ac87dd07452f1615edbc0af4
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/06/2021
ms.locfileid: "115991858"
---
# <a name="convert-a-trial-subscription-to-paid-using-partner-center-apis"></a>Konwertowanie subskrypcji próbnej na płatną przy użyciu Partner Center API

Subskrypcję wersji próbnej można przekonwertować na płatną.

## <a name="prerequisites"></a>Wymagania wstępne

- Poświadczenia zgodnie z opisem w [te Partner Center uwierzytelniania.](partner-center-authentication.md) Ten scenariusz obsługuje uwierzytelnianie tylko przy użyciu poświadczeń aplikacji i użytkownika.

- Identyfikator klienta ( `customer-tenant-id` ). Jeśli nie znasz identyfikatora klienta, możesz go znaleźć na pulpicie nawigacyjnym Partner Center [nawigacyjnym](https://partner.microsoft.com/dashboard). Wybierz **pozycję CSP** z menu Partner Center, a następnie pozycję **Klienci.** Wybierz klienta z listy klientów, a następnie wybierz **pozycję Konto**. Na stronie Konto klienta poszukaj identyfikatora **Microsoft w** sekcji Informacje o **koncie** klienta. Identyfikator microsoft jest taki sam jak identyfikator klienta ( `customer-tenant-id` ).

- Identyfikator subskrypcji dla aktywnej subskrypcji wersji próbnej.

- Dostępna oferta konwersji.

## <a name="convert-a-trial-subscription-to-a-paid-subscription-through-code"></a>Konwertowanie subskrypcji wersji próbnej na płatną subskrypcję za pomocą kodu

Aby przekonwertować subskrypcję wersji próbnej na płatną, musisz najpierw uzyskać kolekcję dostępnych konwersji wersji próbnej. Następnie należy wybrać ofertę konwersji, którą chcesz kupić.

Oferty konwersji określają domyślną liczbę licencji, która jest taka sama jak w przypadku subskrypcji wersji próbnej. Możesz zmienić tę ilość, ustawiając właściwość [**Quantity**](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.conversion.quantity) na liczbę licencji, które chcesz kupić.

> [!NOTE]
> Niezależnie od liczby zakupionych licencji identyfikator subskrypcji wersji próbnej jest ponownie wykorzystywany dla zakupionych licencji. W związku z tym okres próbny znika i jest zastępowany zakupem.

Aby przekonwertować subskrypcję wersji próbnej za pomocą kodu, należy wykonać następujące czynności:

1. Uzyskiwanie interfejsu do dostępnych operacji subskrypcji. Należy zidentyfikować klienta i określić identyfikator subskrypcji wersji próbnej.

    ``` csharp
    var subscriptionOperations = partnerOperations.Customers.ById(customerId).Subscriptions.ById(subscriptionId);
    ```

2. Pobierz kolekcję dostępnych ofert konwersji. Aby uzyskać więcej informacji i szczegółów dotyczących żądania/odpowiedzi dla tej metody, zobacz Get a list of trial conversion offers (Uzyskiwanie listy ofert konwersji w wersji [próbnej).](get-a-list-of-trial-conversion-offers.md)

    ``` csharp
    var conversions = subscriptionOperations.Conversions.Get();
    ```

3. Wybierz ofertę konwersji. Poniższy kod wybiera pierwszą ofertę konwersji w kolekcji.

    ``` csharp
    var selectedConversion = conversions.Items.ToList()[0];
    ```

4. Opcjonalnie określ liczbę licencji do zakupu. Wartość domyślna to liczba licencji w subskrypcji wersji próbnej.

    ``` csharp
    selectedConversion.Quantity = 10;
    ```

5. Wywołaj [**metodę Create**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionupgradecollection.create) lub [**CreateAsync,**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionupgradecollection.createasync) aby przekonwertować subskrypcję wersji próbnej na płatną.

    ``` csharp
    var convertResult = subscriptionOperations.Conversions.Create(selectedConversion);
    ```

## <a name="c"></a>C\#

Aby przekonwertować subskrypcję wersji próbnej na płatną:

1. Użyj metody [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) z identyfikatorem klienta, aby zidentyfikować klienta.

2. Uzyskaj interfejs do operacji subskrypcji, wywołując metodę [**Subscriptions.ById**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.byid) z identyfikatorem subskrypcji wersji próbnej. Zapisz odwołanie do interfejsu operacji subskrypcji w zmiennej lokalnej.

3. Użyj właściwości [**Conversions,**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscription.conversions) aby uzyskać interfejs dostępnych operacji na konwersjach, a następnie wywołaj metodę [**Get**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionconversioncollection.get) lub [**GetAsync,**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionconversioncollection.getasync) aby pobrać kolekcję dostępnych [**ofert konwersji.**](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.conversion) Musisz wybrać jedną z nich. W poniższym przykładzie domyślna jest pierwsza dostępna konwersja.

4. Użyj odwołania do interfejsu operacji subskrypcji zapisanego w zmiennej lokalnej i właściwości [**Conversions,**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscription.conversions) aby uzyskać interfejs do dostępnych operacji na konwersjach.

5. Przekaż wybrany obiekt oferty konwersji do [**metody Create**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionupgradecollection.create) lub [**CreateAsync,**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionupgradecollection.createasync) aby spróbować przetworzyć wersję próbną.

### <a name="c-example"></a>Przykład języka C \#

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
| **Post** | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/subscriptions/{subscription-id}/conversions HTTP/1.1 |

### <a name="uri-parameter"></a>Parametr URI

Użyj następujących parametrów ścieżki, aby zidentyfikować klienta i subskrypcję wersji próbnej.

| Nazwa            | Typ   | Wymagane | Opis                                                     |
|-----------------|--------|----------|-----------------------------------------------------------------|
| identyfikator klienta     | ciąg | Tak      | Ciąg w formacie IDENTYFIKATORA GUID, który identyfikuje klienta.           |
| subscription-id | ciąg | Tak      | Ciąg w formacie IDENTYFIKATORA GUID, który identyfikuje subskrypcję wersji próbnej. |

### <a name="request-headers"></a>Nagłówki żądań

Aby uzyskać więcej informacji, [zobacz Partner Center REST headers (Nagłówki REST).](headers.md)

### <a name="request-body"></a>Treść żądania

Wypełniony zasób [konwersji](conversions-resources.md#conversion) musi zostać uwzględniony w treści żądania.

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

Jeśli to się powiedzie, treść odpowiedzi zawiera [zasób ConversionResult.](conversions-resources.md#conversionresult)

#### <a name="response-success-and-error-codes"></a>Kody powodzenia i błędów odpowiedzi

Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie, oraz dodatkowe informacje o debugowaniu. Użyj narzędzia śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry. Aby uzyskać pełną listę, zobacz [Partner Center kodów błędów](error-codes.md).

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
