---
title: Anulowanie subskrypcji platformy handlowej
description: Dowiedz się, jak za pomocą Partner Center api anulować zasób subskrypcji platformy handlowej, który odpowiada identyfikatorowi klienta i subskrypcji.
ms.date: 08/16/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 95fa265a3c103d1ec55066f12a3ede7fdb2d0170
ms.sourcegitcommit: ad8082bee01fb1f57da423b417ca1ca9c0df8e45
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/10/2021
ms.locfileid: "111974288"
---
# <a name="cancel-a-commercial-marketplace-subscription-using-partner-center-apis"></a><span data-ttu-id="d53c7-103">Anulowanie subskrypcji platformy handlowej przy użyciu Partner Center API</span><span class="sxs-lookup"><span data-stu-id="d53c7-103">Cancel a commercial marketplace subscription using Partner Center APIs</span></span>

<span data-ttu-id="d53c7-104">W tym artykule opisano, jak można użyć interfejsu API Partner Center, aby anulować zasób subskrypcji platformy handlowej pasujący do klienta i identyfikatora subskrypcji. [](subscription-resources.md)</span><span class="sxs-lookup"><span data-stu-id="d53c7-104">This article describes how you can use Partner Center API to cancel a commercial marketplace [subscription](subscription-resources.md) resource that matches the customer and subscription ID.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d53c7-105">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="d53c7-105">Prerequisites</span></span>

- <span data-ttu-id="d53c7-106">Poświadczenia zgodnie z opisem w te [Partner Center uwierzytelniania.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="d53c7-106">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="d53c7-107">Ten scenariusz obsługuje uwierzytelnianie przy użyciu zarówno poświadczeń aplikacji autonomicznej, jak i aplikacji i użytkownika.</span><span class="sxs-lookup"><span data-stu-id="d53c7-107">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="d53c7-108">Identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="d53c7-108">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="d53c7-109">Jeśli nie znasz identyfikatora klienta, możesz go znaleźć na pulpicie nawigacyjnym Partner Center [nawigacyjnym](https://partner.microsoft.com/dashboard).</span><span class="sxs-lookup"><span data-stu-id="d53c7-109">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="d53c7-110">Wybierz **pozycję CSP** z Partner Center menu, a następnie pozycję **Klienci.**</span><span class="sxs-lookup"><span data-stu-id="d53c7-110">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="d53c7-111">Wybierz klienta z listy klientów, a następnie wybierz pozycję **Konto**.</span><span class="sxs-lookup"><span data-stu-id="d53c7-111">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="d53c7-112">Na stronie Konto klienta odszukaj identyfikator **Microsoft w** **sekcji Informacje o koncie** klienta.</span><span class="sxs-lookup"><span data-stu-id="d53c7-112">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="d53c7-113">Identyfikator microsoft jest taki sam jak identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="d53c7-113">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="d53c7-114">Identyfikator subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="d53c7-114">A subscription ID.</span></span>

## <a name="partner-center-dashboard-method"></a><span data-ttu-id="d53c7-115">Partner Center pulpitu nawigacyjnego</span><span class="sxs-lookup"><span data-stu-id="d53c7-115">Partner Center dashboard method</span></span>

<span data-ttu-id="d53c7-116">Aby anulować subskrypcję platformy handlowej na Partner Center nawigacyjnym:</span><span class="sxs-lookup"><span data-stu-id="d53c7-116">To cancel a commercial marketplace subscription in the Partner Center dashboard:</span></span>

1. <span data-ttu-id="d53c7-117">[Wybierz klienta.](get-a-customer-by-name.md)</span><span class="sxs-lookup"><span data-stu-id="d53c7-117">[Select a customer](get-a-customer-by-name.md).</span></span>

2. <span data-ttu-id="d53c7-118">Wybierz subskrypcję, którą chcesz anulować.</span><span class="sxs-lookup"><span data-stu-id="d53c7-118">Select the subscription that you wish to cancel.</span></span>

3. <span data-ttu-id="d53c7-119">Wybierz opcję **Anuluj subskrypcję,** a następnie wybierz pozycję **Prześlij.**</span><span class="sxs-lookup"><span data-stu-id="d53c7-119">Choose the **Cancel subscription** option, then select **Submit**.</span></span>

## <a name="c"></a><span data-ttu-id="d53c7-120">C\#</span><span class="sxs-lookup"><span data-stu-id="d53c7-120">C\#</span></span>

<span data-ttu-id="d53c7-121">Aby anulować subskrypcję klienta:</span><span class="sxs-lookup"><span data-stu-id="d53c7-121">To cancel a customer's subscription:</span></span>

1. <span data-ttu-id="d53c7-122">[Uzyskaj subskrypcję według identyfikatora](get-a-subscription-by-id.md).</span><span class="sxs-lookup"><span data-stu-id="d53c7-122">[Get the subscription by ID](get-a-subscription-by-id.md).</span></span>

2. <span data-ttu-id="d53c7-123">Zmień właściwość [**Status**](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.subscription.status) subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="d53c7-123">Change the subscription's [**Status**](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.subscription.status) property.</span></span> <span data-ttu-id="d53c7-124">Aby uzyskać informacje na **temat kodów** stanu, [zobacz SubscriptionStatus, wyliczenie](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.subscriptionstatus).</span><span class="sxs-lookup"><span data-stu-id="d53c7-124">For information on **Status** codes, see [SubscriptionStatus enumeration](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.subscriptionstatus).</span></span>

3. <span data-ttu-id="d53c7-125">Po w związku z tym użyj **`IAggregatePartner.Customers`** kolekcji i wywołaj **metodę ById().**</span><span class="sxs-lookup"><span data-stu-id="d53c7-125">After the change is made, use your **`IAggregatePartner.Customers`** collection and call the **ById()** method.</span></span>

4. <span data-ttu-id="d53c7-126">Wywołaj [**właściwość Subscriptions,**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.subscriptions) a następnie [**metodę ById().**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.byid)</span><span class="sxs-lookup"><span data-stu-id="d53c7-126">Call the [**Subscriptions**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.subscriptions) property, followed by the [**ById()**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.byid) method.</span></span>

5. <span data-ttu-id="d53c7-127">Wywołaj **metodę Patch().**</span><span class="sxs-lookup"><span data-stu-id="d53c7-127">Call the **Patch()** method.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// var selectedCustomerId as string;
// Subscription selectedSubscription;

selectedSubscription.Status = SubscriptionStatus.Deleted;
var updatedSubscription = partnerOperations.Customers.ById(selectedCustomerId).Subscriptions.ById(selectedSubscription.Id).Patch(selectedSubscription);
```

### <a name="sample-console-test-app"></a><span data-ttu-id="d53c7-128">Przykładowa aplikacja testowa konsoli</span><span class="sxs-lookup"><span data-stu-id="d53c7-128">Sample console test app</span></span>

<span data-ttu-id="d53c7-129">**Przykład:** [aplikacja testowa konsoli](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="d53c7-129">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="d53c7-130">**Project:** Klasa PartnerSDK.FeatureSample: UpdateSubscription.cs </span><span class="sxs-lookup"><span data-stu-id="d53c7-130">**Project**: PartnerSDK.FeatureSample **Class**: UpdateSubscription.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="d53c7-131">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="d53c7-131">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="d53c7-132">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="d53c7-132">Request syntax</span></span>

| <span data-ttu-id="d53c7-133">Metoda</span><span class="sxs-lookup"><span data-stu-id="d53c7-133">Method</span></span>    | <span data-ttu-id="d53c7-134">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="d53c7-134">Request URI</span></span>                                                                                                                |
|-----------|----------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="d53c7-135">**Patch**</span><span class="sxs-lookup"><span data-stu-id="d53c7-135">**PATCH**</span></span> | <span data-ttu-id="d53c7-136">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{identyfikator-dzierżawy-klienta}/subscriptions/{id-for-subscription} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="d53c7-136">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/subscriptions/{id-for-subscription} HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="d53c7-137">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="d53c7-137">URI parameter</span></span>

<span data-ttu-id="d53c7-138">W tej tabeli wymieniono parametr zapytania wymagany do wstrzymania subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="d53c7-138">This table lists the required query parameter to suspend the subscription.</span></span>

| <span data-ttu-id="d53c7-139">Nazwa</span><span class="sxs-lookup"><span data-stu-id="d53c7-139">Name</span></span>                    | <span data-ttu-id="d53c7-140">Typ</span><span class="sxs-lookup"><span data-stu-id="d53c7-140">Type</span></span>     | <span data-ttu-id="d53c7-141">Wymagane</span><span class="sxs-lookup"><span data-stu-id="d53c7-141">Required</span></span> | <span data-ttu-id="d53c7-142">Opis</span><span class="sxs-lookup"><span data-stu-id="d53c7-142">Description</span></span>                               |
|-------------------------|----------|----------|-------------------------------------------|
| <span data-ttu-id="d53c7-143">**identyfikator dzierżawy klienta**</span><span class="sxs-lookup"><span data-stu-id="d53c7-143">**customer-tenant-id**</span></span>  | <span data-ttu-id="d53c7-144">**guid**</span><span class="sxs-lookup"><span data-stu-id="d53c7-144">**guid**</span></span> | <span data-ttu-id="d53c7-145">Y</span><span class="sxs-lookup"><span data-stu-id="d53c7-145">Y</span></span>        | <span data-ttu-id="d53c7-146">Identyfikator GUID odpowiadający klientowi.</span><span class="sxs-lookup"><span data-stu-id="d53c7-146">A GUID corresponding to the customer.</span></span>     |
| <span data-ttu-id="d53c7-147">**identyfikator subskrypcji**</span><span class="sxs-lookup"><span data-stu-id="d53c7-147">**id-for-subscription**</span></span> | <span data-ttu-id="d53c7-148">**guid**</span><span class="sxs-lookup"><span data-stu-id="d53c7-148">**guid**</span></span> | <span data-ttu-id="d53c7-149">Y</span><span class="sxs-lookup"><span data-stu-id="d53c7-149">Y</span></span>        | <span data-ttu-id="d53c7-150">Identyfikator GUID odpowiadający subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="d53c7-150">A GUID corresponding to the subscription.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="d53c7-151">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="d53c7-151">Request headers</span></span>

<span data-ttu-id="d53c7-152">Aby uzyskać więcej informacji, [zobacz Partner Center REST headers (Nagłówki REST).](headers.md)</span><span class="sxs-lookup"><span data-stu-id="d53c7-152">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="d53c7-153">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="d53c7-153">Request body</span></span>

<span data-ttu-id="d53c7-154">W treści **żądania** wymagany jest pełny zasób Subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="d53c7-154">A full **Subscription** resource is required in the request body.</span></span> <span data-ttu-id="d53c7-155">Upewnij **się, że właściwość Status** została zaktualizowana.</span><span class="sxs-lookup"><span data-stu-id="d53c7-155">Ensure that the **Status** property has been updated.</span></span>

### <a name="request-example"></a><span data-ttu-id="d53c7-156">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="d53c7-156">Request example</span></span>

```http
PATCH https://api.partnercenter.microsoft.com/v1/customers/<customer-tenant-id>/subscriptions/<id-for-subscription> HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: ca7c39f7-1a80-43bc-90d8-ee7d1cad3831
MS-CorrelationId: ec8f62e5-1d92-47e9-8d5d-1924af105f2c
If-Match: <etag>
Content-Type: application/json
Content-Length: 1029
Expect: 100-continue
Connection: Keep-Alive

{
    "id": "6e7aa601-629e-461b-8933-0898c3cc3c7c",
    "offerId": "DZH318Z0BXWC:0001:DZH318Z0BMJX",
    "offerName": "offer Name",
    "friendlyName": "friendly Name",
    "quantity": 1,
    "unitType": "License(s)",
    "hasPurchasableAddons": false,
    "creationDate": "2019-01-04T01:00:12.6647304Z",
    "effectiveStartDate": "2019-01-09T00:21:45.9263727+00:00",
    "commitmentEndDate": "2019-02-08T00:21:45.9263727+00:00",
    "status": "deleted",
    "autoRenewEnabled": false,
    "isTrial": false,
    "billingType": "license",
    "billingCycle": "monthly",
    "termDuration": "P1M",
    "refundOptions": [{
        "type": "Full",
        "expiresAt": "2019-01-10T00:21:45.9263727+00:00"
    }],
    "isMicrosoftProduct": false,
    "partnerId": "",
    "contractType": "subscription",
    "publisherName": "publisher Name",
    "orderId": "ImxjLNL4_fOc-2KoyOxGTZcrlIquzls11",
    "attributes": {"objectType": "Subscription"},
}
```

## <a name="rest-response"></a><span data-ttu-id="d53c7-157">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="d53c7-157">REST response</span></span>

<span data-ttu-id="d53c7-158">W przypadku powodzenia ta metoda zwraca usunięte [właściwości zasobów](subscription-resources.md) subskrypcji w treści odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="d53c7-158">If successful, this method returns deleted [Subscription](subscription-resources.md) resource properties in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="d53c7-159">Kody powodzenia i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="d53c7-159">Response success and error codes</span></span>

<span data-ttu-id="d53c7-160">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie, oraz dodatkowe informacje o debugowaniu.</span><span class="sxs-lookup"><span data-stu-id="d53c7-160">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="d53c7-161">Użyj narzędzia śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="d53c7-161">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="d53c7-162">Aby uzyskać pełną listę, zobacz [Kody błędów](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="d53c7-162">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="d53c7-163">Przykład odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="d53c7-163">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 1322
Content-Type: application/json; charset=utf-8
MS-RequestId: ca7c39f7-1a80-43bc-90d8-ee7d1cad3831
MS-CorrelationId: ec8f62e5-1d92-47e9-8d5d-1924af105f2c
X-Locale: en-US

{
    "id": "6e7aa601-629e-461b-8933-0898c3cc3c7c",
    "offerId": "DZH318Z0BXWC:0001:DZH318Z0BMJX",
    "offerName": "offer Name",
    "friendlyName": "friendly Name",
    "quantity": 1,
    "unitType": "License(s)",
    "hasPurchasableAddons": false,
    "creationDate": "2019-01-04T01:00:12.6647304Z",
    "effectiveStartDate": "2019-01-09T00:21:45.9263727+00:00",
    "commitmentEndDate": "2019-02-08T00:21:45.9263727+00:00",
    "status": "deleted",
    "autoRenewEnabled": false,
    "isTrial": false,
    "billingType": "license",
    "billingCycle": "monthly",
    "termDuration": "P1M",
    "refundOptions": [
        {
            "type": "Full",
            "expiresAt": "2019-01-10T00:21:45.9263727+00:00"
        }
    ],
    "isMicrosoftProduct": false,
    "partnerId": "",
    "contractType": "subscription",
    "links": {
        "product": {
            "uri": "/products/DZH318Z0BXWC?country=US",
            "method": "GET",
            "headers": []
        },
        "sku": {
            "uri": "/products/DZH318Z0BXWC/skus/0001?country=US",
            "method": "GET",
            "headers": []
        },
        "availability": {
            "uri": "/products/DZH318Z0BXWC/skus/0001/availabilities/DZH318Z0BMJX?country=US",
            "method": "GET",
            "headers": []
        },
        "self": {
            "uri": "/customers/5921f00a-32c0-4457-aaa1-e8018c650895/subscriptions/6e7aa601-629e-461b-8933-0898c3cc3c7c",
            "method": "GET",
            "headers": []
        }
    },
    "publisherName": "publishe rName",
    "orderId": "ImxjLNL4_fOc-2KoyOxGTZcrlIquzls11",
    "attributes": {
        "etag": "",
        "objectType": "Subscription"
    }
}
```
