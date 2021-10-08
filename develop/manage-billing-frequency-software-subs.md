---
title: Zarządzanie częstotliwością rozliczeń dla subskrypcji oprogramowania
description: Zaktualizuj częstotliwość rozliczeń dla zasobu subskrypcji, który odpowiada identyfikatorowi klienta i subskrypcji.
ms.date: 02/23/2021
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 3cacfe94868afb0b4c1c93842b187d653dffe64f
ms.sourcegitcommit: 36e88224d0957b7ea6298789c75cdd18fc0f3685
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/07/2021
ms.locfileid: "129664940"
---
# <a name="update-billing-frequency-for-software-subscriptions"></a>Aktualizowanie częstotliwości rozliczeń subskrypcji oprogramowania

**Dotyczy:** Partner Center

Zaktualizuj częstotliwość rozliczeń zasobu [subskrypcji](subscription-resources.md) oprogramowania, który odpowiada identyfikatorowi klienta i subskrypcji.

Na Partner Center nawigacyjnym ta operacja jest wykonywana przez [wybranie klienta](get-a-customer-by-name.md). Następnie wybierz subskrypcję, którą chcesz zaktualizować. Na koniec kliknij pozycję Zarządzaj zaplanowaną zmianą, aby wybrać opcję, a następnie wybierz pozycję **Zapisz.**

## <a name="prerequisites"></a>Wymagania wstępne

- Poświadczenia zgodnie z opisem w te Partner Center [uwierzytelniania.](partner-center-authentication.md) Ten scenariusz obsługuje uwierzytelnianie zarówno przy użyciu autonomicznej aplikacji, jak i poświadczeń aplikacji i użytkownika.

- Identyfikator klienta ( `customer-tenant-id` ). Jeśli nie znasz identyfikatora klienta, możesz go znaleźć na pulpicie nawigacyjnym Partner Center [nawigacyjnym](https://partner.microsoft.com/dashboard). Wybierz **pozycję CSP** z Partner Center menu, a następnie pozycję **Klienci.** Wybierz klienta z listy klientów, a następnie wybierz **pozycję Konto**. Na stronie Konto klienta odszukaj identyfikator **Microsoft w** **sekcji Informacje o koncie** klienta. Identyfikator microsoft jest taki sam jak identyfikator klienta ( `customer-tenant-id` ).

- Identyfikator subskrypcji.

## <a name="c"></a>C\#

Aby zaktualizować subskrypcję oprogramowania [](get-a-subscription-by-id.md)klienta, najpierw pobierz subskrypcję, a następnie ustaw właściwość [**billingCycle**](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.subscription.billingCycle) subskrypcji. Po wejściu zmiany użyj **kolekcji IAggregatePartner.Customers** i wywołaj **metodę ById().** Następnie wywołaj [**właściwość Subscriptions,**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.subscriptions) a następnie metodę [**ById().**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.byid) Następnie zakończ, wywołując **metodę Patch().**

``` csharp
// IAggregatePartner partnerOperations;
// var selectedCustomerId as string;
// Subscription selectedSubscription;

this.Context.ConsoleHelper.StartProgress("Updating subscription scheduled change");
selectedSubscription.ScheduledNextTermInstructions = new ScheduledNextTermInstructions
{
    Product = new ProductTerm
    {
        ProductId = changeToProductId,
        SkuId = changeToSkuId,
        AvailabilityId = changeToAvailabilityId,
        BillingCycle = changeToBillingCycle,
        TermDuration = changeToTermDuration,
    },
    Quantity = changeToQuantity,
};

var updatedSubscription = subscriptionOperations.Patch(selectedSubscription);
```

**Przykład:** [aplikacja testowa konsoli](console-test-app.md). **Project:** PartnerSDK.FeatureSample, **klasa:** UpdateSubscription.cs

## <a name="rest-request"></a>Żądanie REST

### <a name="request-syntax"></a>Składnia żądania

| Metoda    | Identyfikator URI żądania                                                                                                                |
|-----------|----------------------------------------------------------------------------------------------------------------------------|
| **PATCH** | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{identyfikator-dzierżawy-klienta}/subscriptions/{id-for-subscription} HTTP/1.1 |

### <a name="uri-parameter"></a>Parametr URI

W tej tabeli wymieniono parametr zapytania wymagany do wstrzymania subskrypcji.

| Nazwa                    | Typ     | Wymagane | Opis                               |
|-------------------------|----------|----------|-------------------------------------------|
| **identyfikator dzierżawy klienta**  | **IDENTYFIKATOR GUID** | Y        | Identyfikator GUID odpowiadający klientowi.     |
| **identyfikator subskrypcji** | **IDENTYFIKATOR GUID** | Y        | Identyfikator GUID odpowiadający subskrypcji. |

### <a name="request-headers"></a>Nagłówki żądań

Aby uzyskać więcej informacji, [zobacz Partner Center REST headers (Nagłówki REST).](headers.md)

### <a name="request-body"></a>Treść żądania

Pełny komercyjny **zasób subskrypcji** platformy handlowej jest wymagany w treści żądania. Upewnij **się, że właściwość AutoRenewEnabled** została zaktualizowana.

### <a name="request-example-for-a-software-subscription"></a>Przykład żądania dla subskrypcji oprogramowania

```http
{ 
    "id": "d3b7c9a2-9a4b-40b2-b075-6e442909e3e7", 
    "offerId": "DG7GMGF0DVSV:000P:DG7GMGF0F3Q9", 
    "offerName": "Windows Server Remote Desktop Services CAL - 1 User CAL – 3 year", 
    "friendlyName": "Windows Server Remote Desktop Services CAL - 1 User CAL – 3 year", 
    "productType": { 
        "id": "Software", 
        "displayName": "Software" 
    }, 
    "quantity": 1, 
    "unitType": "Licenses", 
    "hasPurchasableAddons": false, 
    "creationDate": "2021-09-14T16:44:14.1210743Z", 
    "effectiveStartDate": "2021-09-14T16:44:03.4609789Z", 
    "commitmentEndDate": "2024-09-13T00:00:00Z", 
    "cancellationAllowedUntilDate": "2021-10-14T23:59:00Z", 
    "status": "active", 
    "autoRenewEnabled": true, 
    "scheduledNextTermInstructions": { 
      "product": { 
         "productId":  "DG7GMGF0DVSV", 
         "skuId":  "000P", 
         "availabilityId":  "DG7GMGF0F3Q9", 
         "billingCycle":  "Annual", 
         "termDuration":  "P3Y" 
        }, 
      "quantity":  1 
     },  // original value = null 
    "isTrial": false, 
    "billingType": "license", 
    "billingCycle": "triennial", 
    "termDuration": "P3Y", 
    "renewalTermDuration": "", 
    "isMicrosoftProduct": true, 
    "partnerId": "", 
    "attentionNeeded": false, 
    "actionTaken": false, 
    "contractType": "subscription", 
    "links": { 
        "product": { 
            "uri": "/products/DG7GMGF0DVSV?country=US", 
            "method": "GET", 
            "headers": [] 
        }, 
        "sku": { 
            "uri": "/products/DG7GMGF0DVSV/skus/000P?country=US", 
            "method": "GET", 
            "headers": [] 
        }, 
        "availability": { 
            "uri": "/products/DG7GMGF0DVSV/skus/000P/availabilities/DG7GMGF0F3Q9?country=US", 
            "method": "GET", 
            "headers": [] 
        }, 
        "self": { 
            "uri": "/customers/1f53d7b3-cd04-43a3-a09f-e52f3eb3c205/subscriptions/d3b7c9a2-9a4b-40b2-b075-6e442909e3e7", 
            "method": "GET", 
            "headers": [] 
        } 
    }, 
    "publisherName": "Microsoft", 
    "orderId": "123456789101", 
    "attributes": { 
        "objectType": "Subscription" 
    } 
} 
```

## <a name="rest-response"></a>Odpowiedź REST

W przypadku powodzenia ta metoda zwraca zaktualizowane [właściwości](subscription-resources.md) zasobów subskrypcji w treści odpowiedzi.

### <a name="response-success-and-error-codes"></a>Kody powodzenia i błędów odpowiedzi

Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie, oraz dodatkowe informacje o debugowaniu. Użyj narzędzia śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry. Aby uzyskać pełną listę, zobacz [Kody błędów](error-codes.md).

### <a name="response-example"></a>Przykład odpowiedzi

```http
{ 
    "id": "d3b7c9a2-9a4b-40b2-b075-6e442909e3e7", 
    "offerId": "DG7GMGF0DVSV:000P:DG7GMGF0F3Q9", 
    "offerName": "Windows Server Remote Desktop Services CAL - 1 User CAL – 3 year", 
    "friendlyName": "Windows Server Remote Desktop Services CAL - 1 User CAL – 3 year", 
    "productType": { 
        "id": "Software", 
        "displayName": "Software" 
    }, 
    "quantity": 1, 
    "unitType": "Licenses", 
    "hasPurchasableAddons": false, 
    "creationDate": "2021-09-14T16:44:14.1210743Z", 
    "effectiveStartDate": "2021-09-14T16:44:03.4609789Z", 
    "commitmentEndDate": "2024-09-13T00:00:00Z", 
    "cancellationAllowedUntilDate": "2021-10-14T23:59:00Z", 
    "status": "active", 
    "autoRenewEnabled": true, 
    "scheduledNextTermInstructions": { 
      "product": { 
         "productId":  "DG7GMGF0DVSV", 
         "skuId":  "000P", 
         "availabilityId":  "DG7GMGF0F3Q9", 
         "billingCycle":  "Annual", 
         "termDuration":  "P3Y" 
        }, 
      "quantity":  1 
     },  // original value = null 

    "isTrial": false, 
    "billingType": "license", 
    "billingCycle": "triennial", 
    "termDuration": "P3Y", 
    "renewalTermDuration": "", 
    "isMicrosoftProduct": true, 
    "partnerId": "", 
    "attentionNeeded": false, 
    "actionTaken": false, 
    "contractType": "subscription", 
    "links": { 
        "product": { 
            "uri": "/products/DG7GMGF0DVSV?country=US", 
            "method": "GET", 
            "headers": [] 
        }, 
        "sku": { 
            "uri": "/products/DG7GMGF0DVSV/skus/000P?country=US", 
            "method": "GET", 
            "headers": [] 
        }, 
        "availability": { 
            "uri": "/products/DG7GMGF0DVSV/skus/000P/availabilities/DG7GMGF0F3Q9?country=US", 
            "method": "GET", 
            "headers": [] 
        }, 
        "self": { 
            "uri": "/customers/1f53d7b3-cd04-43a3-a09f-e52f3eb3c205/subscriptions/d3b7c9a2-9a4b-40b2-b075-6e442909e3e7", 
            "method": "GET", 
            "headers": [] 
        } 
    }, 
    "publisherName": "Microsoft", 
    "orderId": "123456789101", 
    "attributes": { 
        "objectType": "Subscription" 
    } 
} 
```
