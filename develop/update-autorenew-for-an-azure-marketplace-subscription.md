---
title: Aktualizowanie automatycznego odnawiania dla subskrypcji platformy handlowej
description: Zaktualizuj Właściwość autorenew dla zasobu subskrypcji, który odpowiada IDENTYFIKATORowi klienta i subskrypcji.
ms.date: 08/16/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 8dccec57901ea4ea429b74044e3b6c28178c43f6
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/19/2020
ms.locfileid: "97768265"
---
# <a name="update-autorenew-for-a-commercial-marketplace-subscription"></a><span data-ttu-id="2fd67-103">Aktualizowanie automatycznego odnawiania dla subskrypcji platformy handlowej</span><span class="sxs-lookup"><span data-stu-id="2fd67-103">Update autorenew for a commercial marketplace subscription</span></span>

<span data-ttu-id="2fd67-104">**Dotyczy**</span><span class="sxs-lookup"><span data-stu-id="2fd67-104">**Applies To**</span></span>

- <span data-ttu-id="2fd67-105">Centrum partnerskie</span><span class="sxs-lookup"><span data-stu-id="2fd67-105">Partner Center</span></span>

<span data-ttu-id="2fd67-106">Zaktualizuj Właściwość autorenew dla komercyjnego zasobu [subskrypcji](subscription-resources.md) portalu Marketplace, który jest zgodny z identyfikatorem klienta i subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="2fd67-106">Update the autorenew property for a commercial marketplace [Subscription](subscription-resources.md) resource that matches the customer and subscription ID.</span></span>

<span data-ttu-id="2fd67-107">Na pulpicie nawigacyjnym Centrum partnerskiego ta operacja jest wykonywana przez pierwsze [wybranie klienta](get-a-customer-by-name.md).</span><span class="sxs-lookup"><span data-stu-id="2fd67-107">In the Partner Center dashboard, this operation is performed by first [selecting a customer](get-a-customer-by-name.md).</span></span> <span data-ttu-id="2fd67-108">Następnie wybierz subskrypcję, którą chcesz zaktualizować.</span><span class="sxs-lookup"><span data-stu-id="2fd67-108">Then, select the subscription that you wish to update.</span></span> <span data-ttu-id="2fd67-109">Na koniec Przełącz opcję **autoodnawiania** , a następnie wybierz pozycję **Prześlij**.</span><span class="sxs-lookup"><span data-stu-id="2fd67-109">Finally, toggle the **Auto-renew** option, then select **Submit**.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2fd67-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="2fd67-110">Prerequisites</span></span>

- <span data-ttu-id="2fd67-111">Poświadczenia zgodnie z opisem w temacie [uwierzytelnianie w centrum partnerskim](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="2fd67-111">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="2fd67-112">Ten scenariusz obsługuje uwierzytelnianie zarówno w przypadku aplikacji autonomicznych, jak i aplikacji oraz poświadczeń użytkownika.</span><span class="sxs-lookup"><span data-stu-id="2fd67-112">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="2fd67-113">Identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="2fd67-113">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="2fd67-114">Jeśli nie znasz identyfikatora klienta, możesz go wyszukać na [pulpicie nawigacyjnym](https://partner.microsoft.com/dashboard)Centrum partnerskiego.</span><span class="sxs-lookup"><span data-stu-id="2fd67-114">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="2fd67-115">Wybierz pozycję **dostawca CSP** z menu Centrum partnerskiego, po którym znajdują się **klienci**.</span><span class="sxs-lookup"><span data-stu-id="2fd67-115">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="2fd67-116">Wybierz klienta z listy klient, a następnie wybierz pozycję **konto**.</span><span class="sxs-lookup"><span data-stu-id="2fd67-116">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="2fd67-117">Na stronie konto klienta Znajdź **Identyfikator Microsoft** w sekcji **Informacje o koncie klienta** .</span><span class="sxs-lookup"><span data-stu-id="2fd67-117">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="2fd67-118">Identyfikator Microsoft jest taki sam jak identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="2fd67-118">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="2fd67-119">Identyfikator subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="2fd67-119">A subscription ID.</span></span>

## <a name="c"></a><span data-ttu-id="2fd67-120">C\#</span><span class="sxs-lookup"><span data-stu-id="2fd67-120">C\#</span></span>

<span data-ttu-id="2fd67-121">Aby zaktualizować subskrypcję klienta, najpierw [Uzyskaj subskrypcję](get-a-subscription-by-id.md), a następnie ustaw właściwość [**autoRenewEnabled**](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.subscription.autoRenewEnabled) subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="2fd67-121">To update a customer's subscription, first [Get the subscription](get-a-subscription-by-id.md), then set the subscription's [**autoRenewEnabled**](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.subscription.autoRenewEnabled) property.</span></span> <span data-ttu-id="2fd67-122">Po wprowadzeniu zmiany Użyj kolekcji **IAggregatePartner. Customers** i Wywołaj metodę **ById ()** .</span><span class="sxs-lookup"><span data-stu-id="2fd67-122">Once the change is made, use your **IAggregatePartner.Customers** collection and call the **ById()** method.</span></span> <span data-ttu-id="2fd67-123">Następnie Wywołaj Właściwość [**subscriptions**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.subscriptions) , a następnie metodę [**ById ()**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.byid) .</span><span class="sxs-lookup"><span data-stu-id="2fd67-123">Then call the [**Subscriptions**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.subscriptions) property, followed by the [**ById()**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.byid) method.</span></span> <span data-ttu-id="2fd67-124">Następnie Zakończ, wywołując metodę **patch ()** .</span><span class="sxs-lookup"><span data-stu-id="2fd67-124">Then, finish by calling the **Patch()** method.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// var selectedCustomerId as string;
// Subscription selectedSubscription;

// turn off auto renew.
selectedSubscription.AutoRenewEnabled = false;
var updatedSubscription = partnerOperations.Customers.ById(selectedCustomerId).Subscriptions.ById(selectedSubscription.Id).Patch(selectedSubscription);
```

<span data-ttu-id="2fd67-125">**Przykład**: [aplikacja testowa konsoli](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="2fd67-125">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="2fd67-126">**Project**: PartnerSDK. FeatureSample **Klasa**: UpdateSubscription.cs</span><span class="sxs-lookup"><span data-stu-id="2fd67-126">**Project**: PartnerSDK.FeatureSample **Class**: UpdateSubscription.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="2fd67-127">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="2fd67-127">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="2fd67-128">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="2fd67-128">Request syntax</span></span>

| <span data-ttu-id="2fd67-129">Metoda</span><span class="sxs-lookup"><span data-stu-id="2fd67-129">Method</span></span>    | <span data-ttu-id="2fd67-130">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="2fd67-130">Request URI</span></span>                                                                                                                |
|-----------|----------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="2fd67-131">**WYSŁANA**</span><span class="sxs-lookup"><span data-stu-id="2fd67-131">**PATCH**</span></span> | <span data-ttu-id="2fd67-132">[*{baseURL}*](partner-center-rest-urls.md)/V1/Customers/{Customer-tenant-ID}/subscriptions/{ID-for-Subscription} http/1.1</span><span class="sxs-lookup"><span data-stu-id="2fd67-132">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/subscriptions/{id-for-subscription} HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="2fd67-133">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="2fd67-133">URI parameter</span></span>

<span data-ttu-id="2fd67-134">Ta tabela zawiera listę wymaganych parametrów zapytania, aby wstrzymać subskrypcję.</span><span class="sxs-lookup"><span data-stu-id="2fd67-134">This table lists the required query parameter to suspend the subscription.</span></span>

| <span data-ttu-id="2fd67-135">Nazwa</span><span class="sxs-lookup"><span data-stu-id="2fd67-135">Name</span></span>                    | <span data-ttu-id="2fd67-136">Typ</span><span class="sxs-lookup"><span data-stu-id="2fd67-136">Type</span></span>     | <span data-ttu-id="2fd67-137">Wymagane</span><span class="sxs-lookup"><span data-stu-id="2fd67-137">Required</span></span> | <span data-ttu-id="2fd67-138">Opis</span><span class="sxs-lookup"><span data-stu-id="2fd67-138">Description</span></span>                               |
|-------------------------|----------|----------|-------------------------------------------|
| <span data-ttu-id="2fd67-139">**Identyfikator dzierżawy klienta**</span><span class="sxs-lookup"><span data-stu-id="2fd67-139">**customer-tenant-id**</span></span>  | <span data-ttu-id="2fd67-140">**IDENT**</span><span class="sxs-lookup"><span data-stu-id="2fd67-140">**GUID**</span></span> | <span data-ttu-id="2fd67-141">Y</span><span class="sxs-lookup"><span data-stu-id="2fd67-141">Y</span></span>        | <span data-ttu-id="2fd67-142">Identyfikator GUID odpowiadający klientowi.</span><span class="sxs-lookup"><span data-stu-id="2fd67-142">A GUID corresponding to the customer.</span></span>     |
| <span data-ttu-id="2fd67-143">**Identyfikator — dla subskrypcji**</span><span class="sxs-lookup"><span data-stu-id="2fd67-143">**id-for-subscription**</span></span> | <span data-ttu-id="2fd67-144">**IDENT**</span><span class="sxs-lookup"><span data-stu-id="2fd67-144">**GUID**</span></span> | <span data-ttu-id="2fd67-145">Y</span><span class="sxs-lookup"><span data-stu-id="2fd67-145">Y</span></span>        | <span data-ttu-id="2fd67-146">Identyfikator GUID odpowiadający subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="2fd67-146">A GUID corresponding to the subscription.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="2fd67-147">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="2fd67-147">Request headers</span></span>

<span data-ttu-id="2fd67-148">Aby uzyskać więcej informacji, zobacz [nagłówki REST Centrum partnerskiego](headers.md).</span><span class="sxs-lookup"><span data-stu-id="2fd67-148">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="2fd67-149">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="2fd67-149">Request body</span></span>

<span data-ttu-id="2fd67-150">W treści żądania jest wymagany pełny komercyjny zasób **subskrypcji** portalu Marketplace.</span><span class="sxs-lookup"><span data-stu-id="2fd67-150">A full commercial marketplace **Subscription** resource is required in the request body.</span></span> <span data-ttu-id="2fd67-151">Upewnij się, że właściwość **AutoRenewEnabled** została zaktualizowana.</span><span class="sxs-lookup"><span data-stu-id="2fd67-151">Ensure that the **AutoRenewEnabled** property has been updated.</span></span>

### <a name="request-example"></a><span data-ttu-id="2fd67-152">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="2fd67-152">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="2fd67-153">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="2fd67-153">REST response</span></span>

<span data-ttu-id="2fd67-154">Jeśli to się powiedzie, ta metoda zwraca zaktualizowane właściwości zasobów [subskrypcji](subscription-resources.md) w treści odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="2fd67-154">If successful, this method returns updated [Subscription](subscription-resources.md) resource properties in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="2fd67-155">Kody sukcesu i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="2fd67-155">Response success and error codes</span></span>

<span data-ttu-id="2fd67-156">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie i dodatkowe informacje debugowania.</span><span class="sxs-lookup"><span data-stu-id="2fd67-156">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="2fd67-157">Użyj narzędzia do śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="2fd67-157">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="2fd67-158">Aby uzyskać pełną listę, zobacz [kody błędów](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="2fd67-158">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="2fd67-159">Przykład odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="2fd67-159">Response example</span></span>

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
