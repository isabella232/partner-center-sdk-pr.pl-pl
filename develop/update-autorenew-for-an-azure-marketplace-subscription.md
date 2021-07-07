---
title: Aktualizowanie automatycznego odnawiania dla subskrypcji platformy handlowej
description: Zaktualizuj właściwość autorenew zasobu Subskrypcji, która odpowiada identyfikatorowi klienta i subskrypcji.
ms.date: 08/16/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: cc0b4c4bff5e8762ffcc2552b2e9e36bcf93686c
ms.sourcegitcommit: 0b2a62af1765a447addd9c4340c28bc42fdc2747
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/04/2021
ms.locfileid: "111446670"
---
# <a name="update-autorenew-for-a-commercial-marketplace-subscription"></a><span data-ttu-id="7859a-103">Aktualizowanie automatycznego odnawiania dla subskrypcji platformy handlowej</span><span class="sxs-lookup"><span data-stu-id="7859a-103">Update autorenew for a commercial marketplace subscription</span></span>

<span data-ttu-id="7859a-104">Zaktualizuj właściwość autorenew dla zasobu subskrypcji platformy [handlowej,](subscription-resources.md) który jest dopasowany do klienta i identyfikatora subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="7859a-104">Update the autorenew property for a commercial marketplace [Subscription](subscription-resources.md) resource that matches the customer and subscription ID.</span></span>

<span data-ttu-id="7859a-105">Na Partner Center nawigacyjnym ta operacja jest wykonywana przez [wybranie klienta](get-a-customer-by-name.md).</span><span class="sxs-lookup"><span data-stu-id="7859a-105">In the Partner Center dashboard, this operation is performed by first [selecting a customer](get-a-customer-by-name.md).</span></span> <span data-ttu-id="7859a-106">Następnie wybierz subskrypcję, którą chcesz zaktualizować.</span><span class="sxs-lookup"><span data-stu-id="7859a-106">Then, select the subscription that you wish to update.</span></span> <span data-ttu-id="7859a-107">Na koniec przełącz opcję **Automatyczne odnawianie,** a następnie wybierz pozycję **Prześlij.**</span><span class="sxs-lookup"><span data-stu-id="7859a-107">Finally, toggle the **Auto-renew** option, then select **Submit**.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7859a-108">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="7859a-108">Prerequisites</span></span>

- <span data-ttu-id="7859a-109">Poświadczenia zgodnie z opisem w te [Partner Center uwierzytelniania.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="7859a-109">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="7859a-110">Ten scenariusz obsługuje uwierzytelnianie przy użyciu zarówno poświadczeń aplikacji autonomicznej, jak i aplikacji i użytkownika.</span><span class="sxs-lookup"><span data-stu-id="7859a-110">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="7859a-111">Identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="7859a-111">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="7859a-112">Jeśli nie znasz identyfikatora klienta, możesz go znaleźć na pulpicie nawigacyjnym Partner Center [nawigacyjnym](https://partner.microsoft.com/dashboard).</span><span class="sxs-lookup"><span data-stu-id="7859a-112">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="7859a-113">Wybierz **pozycję CSP** z Partner Center menu, a następnie pozycję **Klienci.**</span><span class="sxs-lookup"><span data-stu-id="7859a-113">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="7859a-114">Wybierz klienta z listy klientów, a następnie wybierz pozycję **Konto**.</span><span class="sxs-lookup"><span data-stu-id="7859a-114">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="7859a-115">Na stronie Konto klienta odszukaj identyfikator **Microsoft w** **sekcji Informacje o koncie** klienta.</span><span class="sxs-lookup"><span data-stu-id="7859a-115">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="7859a-116">Identyfikator microsoft jest taki sam jak identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="7859a-116">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="7859a-117">Identyfikator subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="7859a-117">A subscription ID.</span></span>

## <a name="c"></a><span data-ttu-id="7859a-118">C\#</span><span class="sxs-lookup"><span data-stu-id="7859a-118">C\#</span></span>

<span data-ttu-id="7859a-119">Aby zaktualizować subskrypcję klienta, najpierw pobierz [subskrypcję,](get-a-subscription-by-id.md)a następnie ustaw właściwość [**autoRenewEnabled**](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.subscription.autoRenewEnabled) subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="7859a-119">To update a customer's subscription, first [Get the subscription](get-a-subscription-by-id.md), then set the subscription's [**autoRenewEnabled**](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.subscription.autoRenewEnabled) property.</span></span> <span data-ttu-id="7859a-120">Po wejściu zmiany użyj **kolekcji IAggregatePartner.Customers** i wywołaj **metodę ById().**</span><span class="sxs-lookup"><span data-stu-id="7859a-120">Once the change is made, use your **IAggregatePartner.Customers** collection and call the **ById()** method.</span></span> <span data-ttu-id="7859a-121">Następnie wywołaj [**właściwość Subscriptions,**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.subscriptions) a następnie metodę [**ById().**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.byid)</span><span class="sxs-lookup"><span data-stu-id="7859a-121">Then call the [**Subscriptions**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.subscriptions) property, followed by the [**ById()**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.byid) method.</span></span> <span data-ttu-id="7859a-122">Następnie zakończ, wywołując **metodę Patch().**</span><span class="sxs-lookup"><span data-stu-id="7859a-122">Then, finish by calling the **Patch()** method.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// var selectedCustomerId as string;
// Subscription selectedSubscription;

// turn off auto renew.
selectedSubscription.AutoRenewEnabled = false;
var updatedSubscription = partnerOperations.Customers.ById(selectedCustomerId).Subscriptions.ById(selectedSubscription.Id).Patch(selectedSubscription);
```

<span data-ttu-id="7859a-123">**Przykład:** [aplikacja testowa konsoli](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="7859a-123">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="7859a-124">**Project:** Klasa PartnerSDK.FeatureSample: UpdateSubscription.cs </span><span class="sxs-lookup"><span data-stu-id="7859a-124">**Project**: PartnerSDK.FeatureSample **Class**: UpdateSubscription.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="7859a-125">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="7859a-125">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="7859a-126">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="7859a-126">Request syntax</span></span>

| <span data-ttu-id="7859a-127">Metoda</span><span class="sxs-lookup"><span data-stu-id="7859a-127">Method</span></span>    | <span data-ttu-id="7859a-128">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="7859a-128">Request URI</span></span>                                                                                                                |
|-----------|----------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="7859a-129">**Patch**</span><span class="sxs-lookup"><span data-stu-id="7859a-129">**PATCH**</span></span> | <span data-ttu-id="7859a-130">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{identyfikator-dzierżawy-klienta}/subscriptions/{id-for-subscription} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="7859a-130">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/subscriptions/{id-for-subscription} HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="7859a-131">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="7859a-131">URI parameter</span></span>

<span data-ttu-id="7859a-132">W tej tabeli wymieniono parametr zapytania wymagany do wstrzymania subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="7859a-132">This table lists the required query parameter to suspend the subscription.</span></span>

| <span data-ttu-id="7859a-133">Nazwa</span><span class="sxs-lookup"><span data-stu-id="7859a-133">Name</span></span>                    | <span data-ttu-id="7859a-134">Typ</span><span class="sxs-lookup"><span data-stu-id="7859a-134">Type</span></span>     | <span data-ttu-id="7859a-135">Wymagane</span><span class="sxs-lookup"><span data-stu-id="7859a-135">Required</span></span> | <span data-ttu-id="7859a-136">Opis</span><span class="sxs-lookup"><span data-stu-id="7859a-136">Description</span></span>                               |
|-------------------------|----------|----------|-------------------------------------------|
| <span data-ttu-id="7859a-137">**identyfikator dzierżawy klienta**</span><span class="sxs-lookup"><span data-stu-id="7859a-137">**customer-tenant-id**</span></span>  | <span data-ttu-id="7859a-138">**Identyfikator guid**</span><span class="sxs-lookup"><span data-stu-id="7859a-138">**GUID**</span></span> | <span data-ttu-id="7859a-139">Y</span><span class="sxs-lookup"><span data-stu-id="7859a-139">Y</span></span>        | <span data-ttu-id="7859a-140">Identyfikator GUID odpowiadający klientowi.</span><span class="sxs-lookup"><span data-stu-id="7859a-140">A GUID corresponding to the customer.</span></span>     |
| <span data-ttu-id="7859a-141">**identyfikator subskrypcji**</span><span class="sxs-lookup"><span data-stu-id="7859a-141">**id-for-subscription**</span></span> | <span data-ttu-id="7859a-142">**Identyfikator guid**</span><span class="sxs-lookup"><span data-stu-id="7859a-142">**GUID**</span></span> | <span data-ttu-id="7859a-143">Y</span><span class="sxs-lookup"><span data-stu-id="7859a-143">Y</span></span>        | <span data-ttu-id="7859a-144">Identyfikator GUID odpowiadający subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="7859a-144">A GUID corresponding to the subscription.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="7859a-145">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="7859a-145">Request headers</span></span>

<span data-ttu-id="7859a-146">Aby uzyskać więcej informacji, [zobacz Partner Center REST headers (Nagłówki REST).](headers.md)</span><span class="sxs-lookup"><span data-stu-id="7859a-146">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="7859a-147">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="7859a-147">Request body</span></span>

<span data-ttu-id="7859a-148">Pełny komercyjny **zasób subskrypcji** platformy handlowej jest wymagany w treści żądania.</span><span class="sxs-lookup"><span data-stu-id="7859a-148">A full commercial marketplace **Subscription** resource is required in the request body.</span></span> <span data-ttu-id="7859a-149">Upewnij **się, że właściwość AutoRenewEnabled** została zaktualizowana.</span><span class="sxs-lookup"><span data-stu-id="7859a-149">Ensure that the **AutoRenewEnabled** property has been updated.</span></span>

### <a name="request-example"></a><span data-ttu-id="7859a-150">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="7859a-150">Request example</span></span>

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
    "status": "active",
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

## <a name="rest-response"></a><span data-ttu-id="7859a-151">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="7859a-151">REST response</span></span>

<span data-ttu-id="7859a-152">W przypadku powodzenia ta metoda zwraca zaktualizowane [właściwości](subscription-resources.md) zasobów subskrypcji w treści odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="7859a-152">If successful, this method returns updated [Subscription](subscription-resources.md) resource properties in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="7859a-153">Kody powodzenia i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="7859a-153">Response success and error codes</span></span>

<span data-ttu-id="7859a-154">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie, oraz dodatkowe informacje o debugowaniu.</span><span class="sxs-lookup"><span data-stu-id="7859a-154">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="7859a-155">Użyj narzędzia śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="7859a-155">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="7859a-156">Aby uzyskać pełną listę, zobacz [Kody błędów](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="7859a-156">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="7859a-157">Przykład odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="7859a-157">Response example</span></span>

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
    "status": "active",
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
