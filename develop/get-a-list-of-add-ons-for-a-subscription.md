---
title: Pobieranie listy dodatków dla subskrypcji
description: Jak uzyskać kolekcję dodatków, które klient zdecydował dodać do swojej subskrypcji.
ms.date: 07/25/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: amitravat
ms.author: amrava
ms.openlocfilehash: 4e62ad22cf30c34dedfeb628003c695e33b78758
ms.sourcegitcommit: 58801b7a09c19ce57617ec4181a008a673b725f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/22/2020
ms.locfileid: "97768098"
---
# <a name="get-a-list-of-add-ons-for-a-subscription"></a><span data-ttu-id="10dd0-103">Pobieranie listy dodatków dla subskrypcji</span><span class="sxs-lookup"><span data-stu-id="10dd0-103">Get a list of add-ons for a subscription</span></span>

<span data-ttu-id="10dd0-104">**Dotyczy:**</span><span class="sxs-lookup"><span data-stu-id="10dd0-104">**Applies to:**</span></span>

- <span data-ttu-id="10dd0-105">Centrum partnerskie</span><span class="sxs-lookup"><span data-stu-id="10dd0-105">Partner Center</span></span>
- <span data-ttu-id="10dd0-106">Centrum partnerskie obsługiwane przez firmę 21Vianet</span><span class="sxs-lookup"><span data-stu-id="10dd0-106">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="10dd0-107">Centrum partnerskie dla Microsoft Cloud Niemcy</span><span class="sxs-lookup"><span data-stu-id="10dd0-107">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="10dd0-108">Centrum partnerskie Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="10dd0-108">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="10dd0-109">W tym artykule opisano, jak uzyskać zbiór dodatków, które klient zdecydował dodać do zasobu **[subskrypcji](subscription-resources.md)** .</span><span class="sxs-lookup"><span data-stu-id="10dd0-109">This article describes how to get a collection of add-ons that a customer has chosen to add to their **[Subscription](subscription-resources.md)** resource.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="10dd0-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="10dd0-110">Prerequisites</span></span>

- <span data-ttu-id="10dd0-111">Poświadczenia zgodnie z opisem w temacie [uwierzytelnianie w centrum partnerskim](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="10dd0-111">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="10dd0-112">Ten scenariusz obsługuje uwierzytelnianie zarówno w przypadku aplikacji autonomicznych, jak i aplikacji oraz poświadczeń użytkownika.</span><span class="sxs-lookup"><span data-stu-id="10dd0-112">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="10dd0-113">Identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="10dd0-113">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="10dd0-114">Jeśli nie znasz identyfikatora klienta, możesz go wyszukać na [pulpicie nawigacyjnym](https://partner.microsoft.com/dashboard)Centrum partnerskiego.</span><span class="sxs-lookup"><span data-stu-id="10dd0-114">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="10dd0-115">Wybierz pozycję **dostawca CSP** z menu Centrum partnerskiego, po którym znajdują się **klienci**.</span><span class="sxs-lookup"><span data-stu-id="10dd0-115">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="10dd0-116">Wybierz klienta z listy klient, a następnie wybierz pozycję **konto**.</span><span class="sxs-lookup"><span data-stu-id="10dd0-116">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="10dd0-117">Na stronie konto klienta Znajdź **Identyfikator Microsoft** w sekcji **Informacje o koncie klienta** .</span><span class="sxs-lookup"><span data-stu-id="10dd0-117">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="10dd0-118">Identyfikator Microsoft jest taki sam jak identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="10dd0-118">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="10dd0-119">Identyfikator subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="10dd0-119">A subscription ID.</span></span>

## <a name="c"></a><span data-ttu-id="10dd0-120">C\#</span><span class="sxs-lookup"><span data-stu-id="10dd0-120">C\#</span></span>

<span data-ttu-id="10dd0-121">Aby uzyskać listę dodatków dla subskrypcji klienta:</span><span class="sxs-lookup"><span data-stu-id="10dd0-121">To get the list of add-ons for a customer's subscription:</span></span>

1. <span data-ttu-id="10dd0-122">Użyj kolekcji **IAggregatePartner. Customers** , aby wywołać metodę **ById ()** .</span><span class="sxs-lookup"><span data-stu-id="10dd0-122">Use your **IAggregatePartner.Customers** collection to call the **ById()** method.</span></span>

2. <span data-ttu-id="10dd0-123">Wywołaj Właściwość [**subscriptions**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.subscriptions) , a następnie metodę [**ById ()**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.byid) .</span><span class="sxs-lookup"><span data-stu-id="10dd0-123">Call the [**Subscriptions**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.subscriptions) property, followed by the [**ById()**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.byid) method.</span></span>

3. <span data-ttu-id="10dd0-124">Wywołaj Właściwość [**Dodatki**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscription.addons) , a następnie pozycję [**Get ()**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionaddoncollection.get) lub [**GetAsync ()**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionaddoncollection.getasync).</span><span class="sxs-lookup"><span data-stu-id="10dd0-124">Call the [**Addons**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscription.addons) property, followed by [**Get()**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionaddoncollection.get) or [**GetAsync()**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionaddoncollection.getasync).</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// var selectedCustomerId as string;
// var selectedSubscription Subscription;

var subscriptionDetails = partnerOperations.Customers.ById(selectedCustomerId).Subscriptions.ById(selectedSubscription.Id).AddOns.Get();

```

<span data-ttu-id="10dd0-125">Aby zapoznać się z przykładem, zobacz następujące tematy:</span><span class="sxs-lookup"><span data-stu-id="10dd0-125">For an example, see the following:</span></span>

- <span data-ttu-id="10dd0-126">Przykład: [aplikacja testowa konsoli](console-test-app.md)</span><span class="sxs-lookup"><span data-stu-id="10dd0-126">Sample: [Console test app](console-test-app.md)</span></span>
- <span data-ttu-id="10dd0-127">Projekt: **PartnerSDK. FeatureSample**</span><span class="sxs-lookup"><span data-stu-id="10dd0-127">Project: **PartnerSDK.FeatureSample**</span></span>
- <span data-ttu-id="10dd0-128">Klasa: **SubscriptionAddons.cs**</span><span class="sxs-lookup"><span data-stu-id="10dd0-128">Class: **SubscriptionAddons.cs**</span></span>

## <a name="rest-request"></a><span data-ttu-id="10dd0-129">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="10dd0-129">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="10dd0-130">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="10dd0-130">Request syntax</span></span>

| <span data-ttu-id="10dd0-131">Metoda</span><span class="sxs-lookup"><span data-stu-id="10dd0-131">Method</span></span>  | <span data-ttu-id="10dd0-132">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="10dd0-132">Request URI</span></span>                                                                                                                       |
|---------|-----------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="10dd0-133">**Pobierz**</span><span class="sxs-lookup"><span data-stu-id="10dd0-133">**GET**</span></span> | <span data-ttu-id="10dd0-134">[*{baseURL}*](partner-center-rest-urls.md)/V1/Customers/{Customer-tenant-ID}/subscriptions/{ID-for-Subscription}/addons http/1.1</span><span class="sxs-lookup"><span data-stu-id="10dd0-134">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/subscriptions/{id-for-subscription}/addons HTTP/1.1</span></span> |

#### <a name="uri-parameter"></a><span data-ttu-id="10dd0-135">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="10dd0-135">URI parameter</span></span>

<span data-ttu-id="10dd0-136">Ta tabela zawiera listę wymaganych parametrów zapytania, aby uzyskać listę dodatków dla subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="10dd0-136">This table lists the required query parameters to get the list of add-ons for the subscription.</span></span>

| <span data-ttu-id="10dd0-137">Nazwa</span><span class="sxs-lookup"><span data-stu-id="10dd0-137">Name</span></span>                    | <span data-ttu-id="10dd0-138">Typ</span><span class="sxs-lookup"><span data-stu-id="10dd0-138">Type</span></span>     | <span data-ttu-id="10dd0-139">Wymagane</span><span class="sxs-lookup"><span data-stu-id="10dd0-139">Required</span></span> | <span data-ttu-id="10dd0-140">Opis</span><span class="sxs-lookup"><span data-stu-id="10dd0-140">Description</span></span>                               |
|-------------------------|----------|----------|-------------------------------------------|
| <span data-ttu-id="10dd0-141">**Identyfikator dzierżawy klienta**</span><span class="sxs-lookup"><span data-stu-id="10dd0-141">**customer-tenant-id**</span></span>  | <span data-ttu-id="10dd0-142">**guid**</span><span class="sxs-lookup"><span data-stu-id="10dd0-142">**guid**</span></span> | <span data-ttu-id="10dd0-143">Y</span><span class="sxs-lookup"><span data-stu-id="10dd0-143">Y</span></span>        | <span data-ttu-id="10dd0-144">Identyfikator GUID odpowiadający klientowi.</span><span class="sxs-lookup"><span data-stu-id="10dd0-144">A GUID corresponding to the customer.</span></span>     |
| <span data-ttu-id="10dd0-145">**Identyfikator — dla subskrypcji**</span><span class="sxs-lookup"><span data-stu-id="10dd0-145">**id-for-subscription**</span></span> | <span data-ttu-id="10dd0-146">**guid**</span><span class="sxs-lookup"><span data-stu-id="10dd0-146">**guid**</span></span> | <span data-ttu-id="10dd0-147">Y</span><span class="sxs-lookup"><span data-stu-id="10dd0-147">Y</span></span>        | <span data-ttu-id="10dd0-148">Identyfikator GUID odpowiadający subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="10dd0-148">A GUID corresponding to the subscription.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="10dd0-149">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="10dd0-149">Request headers</span></span>

<span data-ttu-id="10dd0-150">Aby uzyskać więcej informacji, zobacz [nagłówki REST Centrum partnerskiego](headers.md).</span><span class="sxs-lookup"><span data-stu-id="10dd0-150">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="10dd0-151">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="10dd0-151">Request body</span></span>

<span data-ttu-id="10dd0-152">Brak.</span><span class="sxs-lookup"><span data-stu-id="10dd0-152">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="10dd0-153">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="10dd0-153">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/<customer-tenant-id>/subscriptions/<id-for-subscription>/addons HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 429902e2-ea2f-4704-b8a0-27fc53c539ba
MS-CorrelationId: c49004b1-224f-4d86-a607-6c8bcc52cfdd
```

## <a name="rest-response"></a><span data-ttu-id="10dd0-154">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="10dd0-154">REST response</span></span>

<span data-ttu-id="10dd0-155">Jeśli to się powiedzie, ta metoda zwraca kolekcję zasobów w treści odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="10dd0-155">If successful, this method returns a collection of resources in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="10dd0-156">Kody sukcesu i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="10dd0-156">Response success and error codes</span></span>

<span data-ttu-id="10dd0-157">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie i dodatkowe informacje debugowania.</span><span class="sxs-lookup"><span data-stu-id="10dd0-157">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="10dd0-158">Użyj narzędzia do śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="10dd0-158">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="10dd0-159">Aby uzyskać pełną listę, zobacz [kody błędów](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="10dd0-159">For a full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="10dd0-160">Przykład odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="10dd0-160">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 73754
Content-Type: application/json
MS-CorrelationId: c49004b1-224f-4d86-a607-6c8bcc52cfdd
MS-RequestId: 16fee928-dc2c-412f-adbb-871f68babf16
Date: Wed, 25 Nov 2015 05:50:45 GMT

{
    "totalCount": 37,
    "items": [{
        "id": "83ef9d05-4169-4ef9-9657-0e86b1eab1de",
        "entitlementId": "42226ed6-070a-4e0f-b80c-4cdfB3e97aa7",
        "friendlyName": "Myofferpurchase",
        "quantity": 1,
        "unitType": "none",
        "creationDate": "2015-11-25T06: 41: 12Z",
        "effectiveStartDate": "2015-11-24T08: 00: 00Z",
        "commitmentEndDate": "2016-12-12T08: 00: 00Z",
        "status": "active",
        "autoRenewEnabled": false,
        "billingType": "none",
        "contractType": "subscription",
        "links": {
            "offer": {
                "uri": "/v1/offers/0CCA44D6-68E9-4762-94EE-31ECE98783B9",
                "method": "GET",
                "headers": []
            },
            "self": {
                "uri": "/subscriptions?key=<key>",
                "method": "GET",
                "headers": []
            }
        },
        "orderId": "6183db3d-6318-4e52-877e-25806e4971be",
        "attributes": {
            "etag": "<etag>",
            "objectType": "Subscription"
        }
    }],
    "attributes": {
        "objectType": "Collection"
    }
}
```
