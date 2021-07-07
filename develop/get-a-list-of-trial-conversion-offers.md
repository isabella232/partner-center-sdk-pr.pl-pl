---
title: Pobieranie listy ofert konwersji wersji próbnej
description: Jak pobrać listę ofert konwersji w wersji próbnej.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 981910560faf7b7957b28e643c09a003826b9cff
ms.sourcegitcommit: b1d6fd0ca93d8a3e30e970844d3164454415f553
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/09/2021
ms.locfileid: "111873925"
---
# <a name="get-a-list-of-trial-conversion-offers"></a><span data-ttu-id="5e626-103">Pobieranie listy ofert konwersji wersji próbnej</span><span class="sxs-lookup"><span data-stu-id="5e626-103">Get a list of trial conversion offers</span></span>

<span data-ttu-id="5e626-104">Jak pobrać listę ofert konwersji w wersji próbnej.</span><span class="sxs-lookup"><span data-stu-id="5e626-104">How to retrieve a list of trial conversion offers.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5e626-105">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="5e626-105">Prerequisites</span></span>

- <span data-ttu-id="5e626-106">Poświadczenia zgodnie z opisem w [te Partner Center uwierzytelniania.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="5e626-106">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="5e626-107">Ten scenariusz obsługuje uwierzytelnianie tylko przy użyciu poświadczeń aplikacji i użytkownika.</span><span class="sxs-lookup"><span data-stu-id="5e626-107">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="5e626-108">Identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="5e626-108">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="5e626-109">Jeśli nie znasz identyfikatora klienta, możesz go znaleźć na pulpicie nawigacyjnym Partner Center [nawigacyjnym](https://partner.microsoft.com/dashboard).</span><span class="sxs-lookup"><span data-stu-id="5e626-109">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="5e626-110">Wybierz **pozycję CSP** z menu Partner Center, a następnie pozycję **Klienci.**</span><span class="sxs-lookup"><span data-stu-id="5e626-110">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="5e626-111">Wybierz klienta z listy klientów, a następnie wybierz **pozycję Konto**.</span><span class="sxs-lookup"><span data-stu-id="5e626-111">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="5e626-112">Na stronie Konto klienta poszukaj identyfikatora **Microsoft w** sekcji Informacje o **koncie** klienta.</span><span class="sxs-lookup"><span data-stu-id="5e626-112">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="5e626-113">Identyfikator microsoft jest taki sam jak identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="5e626-113">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="5e626-114">Identyfikator subskrypcji dla aktywnej subskrypcji wersji próbnej.</span><span class="sxs-lookup"><span data-stu-id="5e626-114">A subscription ID for an active trial subscription.</span></span>

## <a name="c"></a><span data-ttu-id="5e626-115">C\#</span><span class="sxs-lookup"><span data-stu-id="5e626-115">C\#</span></span>

<span data-ttu-id="5e626-116">Aby uzyskać listę dostępnych konwersji w wersji próbnej, zacznij od użycia metody [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) z identyfikatorem klienta w celu zidentyfikowania klienta.</span><span class="sxs-lookup"><span data-stu-id="5e626-116">To get a list of trial conversions available, start by using the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to identify the customer.</span></span> <span data-ttu-id="5e626-117">Następnie uzyskaj interfejs do operacji subskrypcji, wywołując metodę [**Subscriptions.ById**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.byid) z identyfikatorem subskrypcji wersji próbnej.</span><span class="sxs-lookup"><span data-stu-id="5e626-117">Then, get an interface to subscription operations by calling the [**Subscriptions.ById**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.byid) method with the trial subscription ID.</span></span> <span data-ttu-id="5e626-118">Następnie użyj właściwości [**Conversions,**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscription.conversions) aby uzyskać interfejs do dostępnych operacji konwersji, a następnie wywołaj metodę [**Get**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionconversioncollection.get) lub [**GetAsync,**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionconversioncollection.getasync) aby pobrać kolekcję dostępnych [**ofert konwersji.**](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.conversion)</span><span class="sxs-lookup"><span data-stu-id="5e626-118">Next, use the [**Conversions**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscription.conversions) property to obtain an interface to the available operations on conversions, and then call the [**Get**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionconversioncollection.get) or [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionconversioncollection.getasync) method to retrieve a collection of available [**Conversion**](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.conversion) offers.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// string customerId;
// string subscriptionId;

// Get the available conversions.
var conversions =
    partnerOperations.Customers.ById(customerId).Subscriptions.ById(subscriptionId).Conversions.Get();
```

## <a name="rest-request"></a><span data-ttu-id="5e626-119">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="5e626-119">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="5e626-120">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="5e626-120">Request syntax</span></span>

| <span data-ttu-id="5e626-121">Metoda</span><span class="sxs-lookup"><span data-stu-id="5e626-121">Method</span></span>  | <span data-ttu-id="5e626-122">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="5e626-122">Request URI</span></span>                                                                                                                 |
|---------|-----------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="5e626-123">**Pobierz**</span><span class="sxs-lookup"><span data-stu-id="5e626-123">**GET**</span></span> | <span data-ttu-id="5e626-124">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/subscriptions/{subscription-id}/conversions HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="5e626-124">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/subscriptions/{subscription-id}/conversions HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="5e626-125">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="5e626-125">URI parameter</span></span>

<span data-ttu-id="5e626-126">Użyj następujących parametrów ścieżki, aby zidentyfikować klienta i subskrypcję wersji próbnej.</span><span class="sxs-lookup"><span data-stu-id="5e626-126">Use the following path parameters to identify the customer and trial subscription.</span></span>

| <span data-ttu-id="5e626-127">Nazwa</span><span class="sxs-lookup"><span data-stu-id="5e626-127">Name</span></span>            | <span data-ttu-id="5e626-128">Typ</span><span class="sxs-lookup"><span data-stu-id="5e626-128">Type</span></span>   | <span data-ttu-id="5e626-129">Wymagane</span><span class="sxs-lookup"><span data-stu-id="5e626-129">Required</span></span> | <span data-ttu-id="5e626-130">Opis</span><span class="sxs-lookup"><span data-stu-id="5e626-130">Description</span></span>                                                     |
|-----------------|--------|----------|-----------------------------------------------------------------|
| <span data-ttu-id="5e626-131">identyfikator klienta</span><span class="sxs-lookup"><span data-stu-id="5e626-131">customer-id</span></span>     | <span data-ttu-id="5e626-132">ciąg</span><span class="sxs-lookup"><span data-stu-id="5e626-132">string</span></span> | <span data-ttu-id="5e626-133">Tak</span><span class="sxs-lookup"><span data-stu-id="5e626-133">Yes</span></span>      | <span data-ttu-id="5e626-134">Ciąg w formacie IDENTYFIKATORA GUID, który identyfikuje klienta.</span><span class="sxs-lookup"><span data-stu-id="5e626-134">A GUID formatted string that identifies the customer.</span></span>           |
| <span data-ttu-id="5e626-135">subscription-id</span><span class="sxs-lookup"><span data-stu-id="5e626-135">subscription-id</span></span> | <span data-ttu-id="5e626-136">ciąg</span><span class="sxs-lookup"><span data-stu-id="5e626-136">string</span></span> | <span data-ttu-id="5e626-137">Tak</span><span class="sxs-lookup"><span data-stu-id="5e626-137">Yes</span></span>      | <span data-ttu-id="5e626-138">Ciąg w formacie IDENTYFIKATORA GUID, który identyfikuje subskrypcję wersji próbnej.</span><span class="sxs-lookup"><span data-stu-id="5e626-138">A GUID formatted string that identifies the trial subscription.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="5e626-139">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="5e626-139">Request headers</span></span>

<span data-ttu-id="5e626-140">Aby uzyskać więcej informacji, [zobacz Partner Center REST headers (Nagłówki REST).](headers.md)</span><span class="sxs-lookup"><span data-stu-id="5e626-140">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="5e626-141">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="5e626-141">Request body</span></span>

<span data-ttu-id="5e626-142">Brak.</span><span class="sxs-lookup"><span data-stu-id="5e626-142">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="5e626-143">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="5e626-143">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/0c39d6d5-c70d-4c55-bc02-f620844f3fd1/subscriptions/488745B5-2086-4912-802C-6ABB9F7C3638/conversions HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: e17f5bc6-24bf-4cbe-b632-d7fc6cec3058
MS-CorrelationId: 8daa6d54-72ab-4d6b-9c7d-9266d3734a47
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a><span data-ttu-id="5e626-144">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="5e626-144">REST response</span></span>

<span data-ttu-id="5e626-145">Jeśli to się powiedzie, treść odpowiedzi zawiera kolekcję zasobów [konwersji.](conversions-resources.md#conversionresult)</span><span class="sxs-lookup"><span data-stu-id="5e626-145">If successful, the response body contains a collection of [Conversion](conversions-resources.md#conversionresult) resources.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="5e626-146">Kody powodzenia i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="5e626-146">Response success and error codes</span></span>

<span data-ttu-id="5e626-147">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie, oraz dodatkowe informacje o debugowaniu.</span><span class="sxs-lookup"><span data-stu-id="5e626-147">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="5e626-148">Użyj narzędzia śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="5e626-148">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="5e626-149">Aby uzyskać pełną listę, zobacz [Partner Center kodów błędów](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="5e626-149">For the full list, see [Partner Center error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="5e626-150">Przykład odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="5e626-150">Response example</span></span>

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
