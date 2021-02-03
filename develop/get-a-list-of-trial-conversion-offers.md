---
title: Pobieranie listy ofert konwersji wersji próbnej
description: Jak pobrać listę ofert konwersji wersji próbnej.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: e1eadecde9efa0b59fc7790bd474889bb32821dc
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/19/2020
ms.locfileid: "97768234"
---
# <a name="get-a-list-of-trial-conversion-offers"></a><span data-ttu-id="525be-103">Pobieranie listy ofert konwersji wersji próbnej</span><span class="sxs-lookup"><span data-stu-id="525be-103">Get a list of trial conversion offers</span></span>

<span data-ttu-id="525be-104">**Dotyczy**</span><span class="sxs-lookup"><span data-stu-id="525be-104">**Applies To**</span></span>

- <span data-ttu-id="525be-105">Centrum partnerskie</span><span class="sxs-lookup"><span data-stu-id="525be-105">Partner Center</span></span>

<span data-ttu-id="525be-106">Jak pobrać listę ofert konwersji wersji próbnej.</span><span class="sxs-lookup"><span data-stu-id="525be-106">How to retrieve a list of trial conversion offers.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="525be-107">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="525be-107">Prerequisites</span></span>

- <span data-ttu-id="525be-108">Poświadczenia zgodnie z opisem w temacie [uwierzytelnianie w centrum partnerskim](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="525be-108">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="525be-109">Ten scenariusz obsługuje tylko uwierzytelnianie przy użyciu aplikacji i poświadczeń użytkownika.</span><span class="sxs-lookup"><span data-stu-id="525be-109">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="525be-110">Identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="525be-110">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="525be-111">Jeśli nie znasz identyfikatora klienta, możesz go wyszukać na [pulpicie nawigacyjnym](https://partner.microsoft.com/dashboard)Centrum partnerskiego.</span><span class="sxs-lookup"><span data-stu-id="525be-111">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="525be-112">Wybierz pozycję **dostawca CSP** z menu Centrum partnerskiego, po którym znajdują się **klienci**.</span><span class="sxs-lookup"><span data-stu-id="525be-112">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="525be-113">Wybierz klienta z listy klient, a następnie wybierz pozycję **konto**.</span><span class="sxs-lookup"><span data-stu-id="525be-113">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="525be-114">Na stronie konto klienta Znajdź **Identyfikator Microsoft** w sekcji **Informacje o koncie klienta** .</span><span class="sxs-lookup"><span data-stu-id="525be-114">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="525be-115">Identyfikator Microsoft jest taki sam jak identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="525be-115">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="525be-116">Identyfikator subskrypcji aktywnej subskrypcji próbnej.</span><span class="sxs-lookup"><span data-stu-id="525be-116">A subscription ID for an active trial subscription.</span></span>

## <a name="c"></a><span data-ttu-id="525be-117">C\#</span><span class="sxs-lookup"><span data-stu-id="525be-117">C\#</span></span>

<span data-ttu-id="525be-118">Aby uzyskać listę dostępnych konwersji z wersji próbnej, Zacznij od użycia metody [**IAggregatePartner. Customers. ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) z identyfikatorem klienta, aby zidentyfikować klienta.</span><span class="sxs-lookup"><span data-stu-id="525be-118">To get a list of trial conversions available, start by using the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to identify the customer.</span></span> <span data-ttu-id="525be-119">Następnie uzyskaj interfejs do operacji subskrybowania, wywołując metodę [**Subscription. ById**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.byid) z identyfikatorem subskrypcji wersji próbnej.</span><span class="sxs-lookup"><span data-stu-id="525be-119">Then, get an interface to subscription operations by calling the [**Subscriptions.ById**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.byid) method with the trial subscription ID.</span></span> <span data-ttu-id="525be-120">Następnie użyj właściwości [**konwersje**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscription.conversions) , aby uzyskać interfejs do dostępnych operacji dla konwersji, a następnie wywołać metodę [**Get**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionconversioncollection.get) lub [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionconversioncollection.getasync) w celu pobrania kolekcji dostępnych ofert [**konwersji**](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.conversion) .</span><span class="sxs-lookup"><span data-stu-id="525be-120">Next, use the [**Conversions**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscription.conversions) property to obtain an interface to the available operations on conversions, and then call the [**Get**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionconversioncollection.get) or [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionconversioncollection.getasync) method to retrieve a collection of available [**Conversion**](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.conversion) offers.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// string customerId;
// string subscriptionId;

// Get the available conversions.
var conversions =
    partnerOperations.Customers.ById(customerId).Subscriptions.ById(subscriptionId).Conversions.Get();
```

## <a name="rest-request"></a><span data-ttu-id="525be-121">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="525be-121">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="525be-122">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="525be-122">Request syntax</span></span>

| <span data-ttu-id="525be-123">Metoda</span><span class="sxs-lookup"><span data-stu-id="525be-123">Method</span></span>  | <span data-ttu-id="525be-124">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="525be-124">Request URI</span></span>                                                                                                                 |
|---------|-----------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="525be-125">**Pobierz**</span><span class="sxs-lookup"><span data-stu-id="525be-125">**GET**</span></span> | <span data-ttu-id="525be-126">[*{baseURL}*](partner-center-rest-urls.md)/V1/Customers/{Customer-ID}/subscriptions/{Subscription-ID}/conversions http/1.1</span><span class="sxs-lookup"><span data-stu-id="525be-126">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/subscriptions/{subscription-id}/conversions HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="525be-127">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="525be-127">URI parameter</span></span>

<span data-ttu-id="525be-128">Użyj następujących parametrów ścieżki, aby zidentyfikować klienta i subskrypcję wersji próbnej.</span><span class="sxs-lookup"><span data-stu-id="525be-128">Use the following path parameters to identify the customer and trial subscription.</span></span>

| <span data-ttu-id="525be-129">Nazwa</span><span class="sxs-lookup"><span data-stu-id="525be-129">Name</span></span>            | <span data-ttu-id="525be-130">Typ</span><span class="sxs-lookup"><span data-stu-id="525be-130">Type</span></span>   | <span data-ttu-id="525be-131">Wymagane</span><span class="sxs-lookup"><span data-stu-id="525be-131">Required</span></span> | <span data-ttu-id="525be-132">Opis</span><span class="sxs-lookup"><span data-stu-id="525be-132">Description</span></span>                                                     |
|-----------------|--------|----------|-----------------------------------------------------------------|
| <span data-ttu-id="525be-133">Identyfikator klienta</span><span class="sxs-lookup"><span data-stu-id="525be-133">customer-id</span></span>     | <span data-ttu-id="525be-134">ciąg</span><span class="sxs-lookup"><span data-stu-id="525be-134">string</span></span> | <span data-ttu-id="525be-135">Tak</span><span class="sxs-lookup"><span data-stu-id="525be-135">Yes</span></span>      | <span data-ttu-id="525be-136">Ciąg w formacie GUID, który identyfikuje klienta.</span><span class="sxs-lookup"><span data-stu-id="525be-136">A GUID formatted string that identifies the customer.</span></span>           |
| <span data-ttu-id="525be-137">Identyfikator subskrypcji</span><span class="sxs-lookup"><span data-stu-id="525be-137">subscription-id</span></span> | <span data-ttu-id="525be-138">ciąg</span><span class="sxs-lookup"><span data-stu-id="525be-138">string</span></span> | <span data-ttu-id="525be-139">Tak</span><span class="sxs-lookup"><span data-stu-id="525be-139">Yes</span></span>      | <span data-ttu-id="525be-140">Ciąg w formacie GUID, który identyfikuje subskrypcję wersji próbnej.</span><span class="sxs-lookup"><span data-stu-id="525be-140">A GUID formatted string that identifies the trial subscription.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="525be-141">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="525be-141">Request headers</span></span>

<span data-ttu-id="525be-142">Aby uzyskać więcej informacji, zobacz [nagłówki REST Centrum partnerskiego](headers.md).</span><span class="sxs-lookup"><span data-stu-id="525be-142">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="525be-143">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="525be-143">Request body</span></span>

<span data-ttu-id="525be-144">Brak.</span><span class="sxs-lookup"><span data-stu-id="525be-144">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="525be-145">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="525be-145">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/0c39d6d5-c70d-4c55-bc02-f620844f3fd1/subscriptions/488745B5-2086-4912-802C-6ABB9F7C3638/conversions HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: e17f5bc6-24bf-4cbe-b632-d7fc6cec3058
MS-CorrelationId: 8daa6d54-72ab-4d6b-9c7d-9266d3734a47
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a><span data-ttu-id="525be-146">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="525be-146">REST response</span></span>

<span data-ttu-id="525be-147">Jeśli to się powiedzie, treść odpowiedzi zawiera kolekcję zasobów [konwersji](conversions-resources.md#conversionresult) .</span><span class="sxs-lookup"><span data-stu-id="525be-147">If successful, the response body contains a collection of [Conversion](conversions-resources.md#conversionresult) resources.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="525be-148">Kody sukcesu i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="525be-148">Response success and error codes</span></span>

<span data-ttu-id="525be-149">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie i dodatkowe informacje debugowania.</span><span class="sxs-lookup"><span data-stu-id="525be-149">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="525be-150">Użyj narzędzia do śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="525be-150">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="525be-151">Aby uzyskać pełną listę, zobacz [kody błędów Centrum partnerskiego](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="525be-151">For the full list, see [Partner Center error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="525be-152">Przykład odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="525be-152">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 305
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 8daa6d54-72ab-4d6b-9c7d-9266d3734a47
MS-RequestId: e17f5bc6-24bf-4cbe-b632-d7fc6cec3058
MS-CV: feJByqU1X0ObaTQr.0
MS-ServerId: 030011719
Date: Thu, 15 Jun 2017 23:10:01 GMT

 {
    "totalCount": 1,
    "items": [{
            "offerId": "C0BD2E08-11AC-4836-BDC7-3712E744922F",
            "targetOfferId": "031C9E47-4802-4248-838E-778FB1D2CC05",
            "orderId": "D51A052E-043C-4A2A-AA37-2BB938CEF6C1",
            "quantity": 25,
            "billingCycle": "monthly",
            "attributes": {
                "objectType": "Conversion"
            }
        }
    ],
    "attributes": {
        "objectType": "Collection"
    }
}
```
