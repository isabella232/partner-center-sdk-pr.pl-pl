---
title: Anulowanie subskrypcji platformy handlowej
description: Dowiedz się, jak za pomocą interfejsów API usługi Partner Center anulować zasób komercyjnej subskrypcji portalu Marketplace, który jest zgodny z IDENTYFIKATORem klienta i subskrypcji.
ms.date: 08/16/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 38708c17b31e39a5e7c436e0d76b4ebabbc3a801
ms.sourcegitcommit: a25d4951f25502cdf90cfb974022c5e452205f42
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/04/2020
ms.locfileid: "97768593"
---
# <a name="cancel-a-commercial-marketplace-subscription-using-partner-center-apis"></a><span data-ttu-id="f0901-103">Anulowanie komercyjnej subskrypcji portalu Marketplace przy użyciu interfejsów API Centrum partnerskiego</span><span class="sxs-lookup"><span data-stu-id="f0901-103">Cancel a commercial marketplace subscription using Partner Center APIs</span></span>

<span data-ttu-id="f0901-104">**Dotyczy:**</span><span class="sxs-lookup"><span data-stu-id="f0901-104">**Applies to:**</span></span>

- <span data-ttu-id="f0901-105">Centrum partnerskie</span><span class="sxs-lookup"><span data-stu-id="f0901-105">Partner Center</span></span>

<span data-ttu-id="f0901-106">W tym artykule opisano, jak można użyć interfejsu API Centrum partnerskiego w celu anulowania komercyjnego zasobu [subskrypcji](subscription-resources.md) portalu Marketplace, który jest zgodny z identyfikatorem klienta i subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="f0901-106">This article describes how you can use Partner Center API to cancel a commercial marketplace [subscription](subscription-resources.md) resource that matches the customer and subscription ID.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f0901-107">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="f0901-107">Prerequisites</span></span>

- <span data-ttu-id="f0901-108">Poświadczenia zgodnie z opisem w temacie [uwierzytelnianie w centrum partnerskim](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="f0901-108">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="f0901-109">Ten scenariusz obsługuje uwierzytelnianie zarówno w przypadku aplikacji autonomicznych, jak i aplikacji oraz poświadczeń użytkownika.</span><span class="sxs-lookup"><span data-stu-id="f0901-109">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="f0901-110">Identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="f0901-110">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="f0901-111">Jeśli nie znasz identyfikatora klienta, możesz go wyszukać na [pulpicie nawigacyjnym](https://partner.microsoft.com/dashboard)Centrum partnerskiego.</span><span class="sxs-lookup"><span data-stu-id="f0901-111">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="f0901-112">Wybierz pozycję **dostawca CSP** z menu Centrum partnerskiego, po którym znajdują się **klienci**.</span><span class="sxs-lookup"><span data-stu-id="f0901-112">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="f0901-113">Wybierz klienta z listy klient, a następnie wybierz pozycję **konto**.</span><span class="sxs-lookup"><span data-stu-id="f0901-113">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="f0901-114">Na stronie konto klienta Znajdź **Identyfikator Microsoft** w sekcji **Informacje o koncie klienta** .</span><span class="sxs-lookup"><span data-stu-id="f0901-114">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="f0901-115">Identyfikator Microsoft jest taki sam jak identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="f0901-115">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="f0901-116">Identyfikator subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="f0901-116">A subscription ID.</span></span>

## <a name="partner-center-dashboard-method"></a><span data-ttu-id="f0901-117">Metoda pulpitu nawigacyjnego Centrum partnerskiego</span><span class="sxs-lookup"><span data-stu-id="f0901-117">Partner Center dashboard method</span></span>

<span data-ttu-id="f0901-118">Aby anulować komercyjną subskrypcję portalu Marketplace na pulpicie nawigacyjnym Centrum partnerskiego:</span><span class="sxs-lookup"><span data-stu-id="f0901-118">To cancel a commercial marketplace subscription in the Partner Center dashboard:</span></span>

1. <span data-ttu-id="f0901-119">[Wybierz klienta](get-a-customer-by-name.md).</span><span class="sxs-lookup"><span data-stu-id="f0901-119">[Select a customer](get-a-customer-by-name.md).</span></span>

2. <span data-ttu-id="f0901-120">Wybierz subskrypcję, którą chcesz anulować.</span><span class="sxs-lookup"><span data-stu-id="f0901-120">Select the subscription that you wish to cancel.</span></span>

3. <span data-ttu-id="f0901-121">Wybierz opcję **Anuluj subskrypcję** , a następnie wybierz pozycję **Prześlij**.</span><span class="sxs-lookup"><span data-stu-id="f0901-121">Choose the **Cancel subscription** option, then select **Submit**.</span></span>

## <a name="c"></a><span data-ttu-id="f0901-122">C\#</span><span class="sxs-lookup"><span data-stu-id="f0901-122">C\#</span></span>

<span data-ttu-id="f0901-123">Aby anulować subskrypcję klienta:</span><span class="sxs-lookup"><span data-stu-id="f0901-123">To cancel a customer's subscription:</span></span>

1. <span data-ttu-id="f0901-124">[Pobierz subskrypcję według identyfikatora](get-a-subscription-by-id.md).</span><span class="sxs-lookup"><span data-stu-id="f0901-124">[Get the subscription by ID](get-a-subscription-by-id.md).</span></span>

2. <span data-ttu-id="f0901-125">Zmień wartość właściwości [**stan**](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.subscription.status) subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="f0901-125">Change the subscription's [**Status**](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.subscription.status) property.</span></span> <span data-ttu-id="f0901-126">Aby uzyskać informacje na temat kodów **stanu** , zobacz [Wyliczenie SubscriptionStatus](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.subscriptionstatus).</span><span class="sxs-lookup"><span data-stu-id="f0901-126">For information on **Status** codes, see [SubscriptionStatus enumeration](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.subscriptionstatus).</span></span>

3. <span data-ttu-id="f0901-127">Po wprowadzeniu zmiany Użyj **`IAggregatePartner.Customers`** kolekcji i Wywołaj metodę **ById ()** .</span><span class="sxs-lookup"><span data-stu-id="f0901-127">After the change is made, use your **`IAggregatePartner.Customers`** collection and call the **ById()** method.</span></span>

4. <span data-ttu-id="f0901-128">Wywołaj Właściwość [**subscriptions**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.subscriptions) , a następnie metodę [**ById ()**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.byid) .</span><span class="sxs-lookup"><span data-stu-id="f0901-128">Call the [**Subscriptions**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.subscriptions) property, followed by the [**ById()**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.byid) method.</span></span>

5. <span data-ttu-id="f0901-129">Wywołaj metodę **patch ()** .</span><span class="sxs-lookup"><span data-stu-id="f0901-129">Call the **Patch()** method.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// var selectedCustomerId as string;
// Subscription selectedSubscription;

selectedSubscription.Status = SubscriptionStatus.Deleted;
var updatedSubscription = partnerOperations.Customers.ById(selectedCustomerId).Subscriptions.ById(selectedSubscription.Id).Patch(selectedSubscription);
```

### <a name="sample-console-test-app"></a><span data-ttu-id="f0901-130">Przykładowa aplikacja testowa konsoli</span><span class="sxs-lookup"><span data-stu-id="f0901-130">Sample console test app</span></span>

<span data-ttu-id="f0901-131">**Przykład**: [aplikacja testowa konsoli](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="f0901-131">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="f0901-132">**Project**: PartnerSDK. FeatureSample **Klasa**: UpdateSubscription.cs</span><span class="sxs-lookup"><span data-stu-id="f0901-132">**Project**: PartnerSDK.FeatureSample **Class**: UpdateSubscription.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="f0901-133">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="f0901-133">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="f0901-134">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="f0901-134">Request syntax</span></span>

| <span data-ttu-id="f0901-135">Metoda</span><span class="sxs-lookup"><span data-stu-id="f0901-135">Method</span></span>    | <span data-ttu-id="f0901-136">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="f0901-136">Request URI</span></span>                                                                                                                |
|-----------|----------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="f0901-137">**WYSŁANA**</span><span class="sxs-lookup"><span data-stu-id="f0901-137">**PATCH**</span></span> | <span data-ttu-id="f0901-138">[*{baseURL}*](partner-center-rest-urls.md)/V1/Customers/{Customer-tenant-ID}/subscriptions/{ID-for-Subscription} http/1.1</span><span class="sxs-lookup"><span data-stu-id="f0901-138">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/subscriptions/{id-for-subscription} HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="f0901-139">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="f0901-139">URI parameter</span></span>

<span data-ttu-id="f0901-140">Ta tabela zawiera listę wymaganych parametrów zapytania, aby wstrzymać subskrypcję.</span><span class="sxs-lookup"><span data-stu-id="f0901-140">This table lists the required query parameter to suspend the subscription.</span></span>

| <span data-ttu-id="f0901-141">Nazwa</span><span class="sxs-lookup"><span data-stu-id="f0901-141">Name</span></span>                    | <span data-ttu-id="f0901-142">Typ</span><span class="sxs-lookup"><span data-stu-id="f0901-142">Type</span></span>     | <span data-ttu-id="f0901-143">Wymagane</span><span class="sxs-lookup"><span data-stu-id="f0901-143">Required</span></span> | <span data-ttu-id="f0901-144">Opis</span><span class="sxs-lookup"><span data-stu-id="f0901-144">Description</span></span>                               |
|-------------------------|----------|----------|-------------------------------------------|
| <span data-ttu-id="f0901-145">**Identyfikator dzierżawy klienta**</span><span class="sxs-lookup"><span data-stu-id="f0901-145">**customer-tenant-id**</span></span>  | <span data-ttu-id="f0901-146">**guid**</span><span class="sxs-lookup"><span data-stu-id="f0901-146">**guid**</span></span> | <span data-ttu-id="f0901-147">Y</span><span class="sxs-lookup"><span data-stu-id="f0901-147">Y</span></span>        | <span data-ttu-id="f0901-148">Identyfikator GUID odpowiadający klientowi.</span><span class="sxs-lookup"><span data-stu-id="f0901-148">A GUID corresponding to the customer.</span></span>     |
| <span data-ttu-id="f0901-149">**Identyfikator — dla subskrypcji**</span><span class="sxs-lookup"><span data-stu-id="f0901-149">**id-for-subscription**</span></span> | <span data-ttu-id="f0901-150">**guid**</span><span class="sxs-lookup"><span data-stu-id="f0901-150">**guid**</span></span> | <span data-ttu-id="f0901-151">Y</span><span class="sxs-lookup"><span data-stu-id="f0901-151">Y</span></span>        | <span data-ttu-id="f0901-152">Identyfikator GUID odpowiadający subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="f0901-152">A GUID corresponding to the subscription.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="f0901-153">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="f0901-153">Request headers</span></span>

<span data-ttu-id="f0901-154">Aby uzyskać więcej informacji, zobacz [nagłówki REST Centrum partnerskiego](headers.md).</span><span class="sxs-lookup"><span data-stu-id="f0901-154">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="f0901-155">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="f0901-155">Request body</span></span>

<span data-ttu-id="f0901-156">W treści żądania jest wymagany pełny zasób **subskrypcji** .</span><span class="sxs-lookup"><span data-stu-id="f0901-156">A full **Subscription** resource is required in the request body.</span></span> <span data-ttu-id="f0901-157">Upewnij się, że właściwość **status** została zaktualizowana.</span><span class="sxs-lookup"><span data-stu-id="f0901-157">Ensure that the **Status** property has been updated.</span></span>

### <a name="request-example"></a><span data-ttu-id="f0901-158">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="f0901-158">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="f0901-159">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="f0901-159">REST response</span></span>

<span data-ttu-id="f0901-160">Jeśli to się powiedzie, ta metoda zwróci usunięte właściwości zasobów [subskrypcji](subscription-resources.md) w treści odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="f0901-160">If successful, this method returns deleted [Subscription](subscription-resources.md) resource properties in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="f0901-161">Kody sukcesu i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="f0901-161">Response success and error codes</span></span>

<span data-ttu-id="f0901-162">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie i dodatkowe informacje debugowania.</span><span class="sxs-lookup"><span data-stu-id="f0901-162">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="f0901-163">Użyj narzędzia do śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="f0901-163">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="f0901-164">Aby uzyskać pełną listę, zobacz [kody błędów](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="f0901-164">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="f0901-165">Przykład odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="f0901-165">Response example</span></span>

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
