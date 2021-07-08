---
title: Pobieranie listy dodatków dla subskrypcji
description: Jak uzyskać kolekcję dodatków, które klient wybrał do dodania do swojej subskrypcji.
ms.date: 07/25/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: amitravat
ms.author: amrava
ms.openlocfilehash: c627f595333a295048b02ec4326dcdc279d07b51
ms.sourcegitcommit: b1d6fd0ca93d8a3e30e970844d3164454415f553
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/09/2021
ms.locfileid: "111874639"
---
# <a name="get-a-list-of-add-ons-for-a-subscription"></a><span data-ttu-id="fd0c8-103">Pobieranie listy dodatków dla subskrypcji</span><span class="sxs-lookup"><span data-stu-id="fd0c8-103">Get a list of add-ons for a subscription</span></span>

<span data-ttu-id="fd0c8-104">**Dotyczy:** Partner Center | Partner Center obsługiwana przez firmę 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="fd0c8-104">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="fd0c8-105">W tym artykule opisano sposób pobierania kolekcji dodatków, które klient wybrał do dodania do **[swojego zasobu subskrypcji.](subscription-resources.md)**</span><span class="sxs-lookup"><span data-stu-id="fd0c8-105">This article describes how to get a collection of add-ons that a customer has chosen to add to their **[Subscription](subscription-resources.md)** resource.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="fd0c8-106">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="fd0c8-106">Prerequisites</span></span>

- <span data-ttu-id="fd0c8-107">Poświadczenia zgodnie z opisem w [te Partner Center uwierzytelniania.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="fd0c8-107">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="fd0c8-108">Ten scenariusz obsługuje uwierzytelnianie przy użyciu zarówno poświadczeń aplikacji autonomicznej, jak i aplikacji i użytkownika.</span><span class="sxs-lookup"><span data-stu-id="fd0c8-108">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="fd0c8-109">Identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="fd0c8-109">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="fd0c8-110">Jeśli nie znasz identyfikatora klienta, możesz go znaleźć na pulpicie nawigacyjnym Partner Center [nawigacyjnym](https://partner.microsoft.com/dashboard).</span><span class="sxs-lookup"><span data-stu-id="fd0c8-110">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="fd0c8-111">Wybierz **pozycję CSP** z menu Partner Center, a następnie pozycję **Klienci.**</span><span class="sxs-lookup"><span data-stu-id="fd0c8-111">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="fd0c8-112">Wybierz klienta z listy klientów, a następnie wybierz **pozycję Konto**.</span><span class="sxs-lookup"><span data-stu-id="fd0c8-112">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="fd0c8-113">Na stronie Konto klienta poszukaj identyfikatora **Microsoft w** sekcji Informacje o **koncie** klienta.</span><span class="sxs-lookup"><span data-stu-id="fd0c8-113">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="fd0c8-114">Identyfikator microsoft jest taki sam jak identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="fd0c8-114">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="fd0c8-115">Identyfikator subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="fd0c8-115">A subscription ID.</span></span>

## <a name="c"></a><span data-ttu-id="fd0c8-116">C\#</span><span class="sxs-lookup"><span data-stu-id="fd0c8-116">C\#</span></span>

<span data-ttu-id="fd0c8-117">Aby uzyskać listę dodatków dla subskrypcji klienta:</span><span class="sxs-lookup"><span data-stu-id="fd0c8-117">To get the list of add-ons for a customer's subscription:</span></span>

1. <span data-ttu-id="fd0c8-118">Użyj **kolekcji IAggregatePartner.Customers,** aby wywołać **metodę ById().**</span><span class="sxs-lookup"><span data-stu-id="fd0c8-118">Use your **IAggregatePartner.Customers** collection to call the **ById()** method.</span></span>

2. <span data-ttu-id="fd0c8-119">Wywołaj [**właściwość Subscriptions,**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.subscriptions) a następnie metodę [**ById().**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.byid)</span><span class="sxs-lookup"><span data-stu-id="fd0c8-119">Call the [**Subscriptions**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.subscriptions) property, followed by the [**ById()**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.byid) method.</span></span>

3. <span data-ttu-id="fd0c8-120">Wywołaj [**właściwość Addons,**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscription.addons) a następnie [**pozycję Get()**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionaddoncollection.get) lub [**GetAsync()**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionaddoncollection.getasync).</span><span class="sxs-lookup"><span data-stu-id="fd0c8-120">Call the [**Addons**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscription.addons) property, followed by [**Get()**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionaddoncollection.get) or [**GetAsync()**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionaddoncollection.getasync).</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// var selectedCustomerId as string;
// var selectedSubscription Subscription;

var subscriptionDetails = partnerOperations.Customers.ById(selectedCustomerId).Subscriptions.ById(selectedSubscription.Id).AddOns.Get();

```

<span data-ttu-id="fd0c8-121">Przykład można znaleźć w następujących tematach:</span><span class="sxs-lookup"><span data-stu-id="fd0c8-121">For an example, see the following:</span></span>

- <span data-ttu-id="fd0c8-122">Przykład: [aplikacja testowa konsoli](console-test-app.md)</span><span class="sxs-lookup"><span data-stu-id="fd0c8-122">Sample: [Console test app](console-test-app.md)</span></span>
- <span data-ttu-id="fd0c8-123">Project: **PartnerSDK.FeatureSample**</span><span class="sxs-lookup"><span data-stu-id="fd0c8-123">Project: **PartnerSDK.FeatureSample**</span></span>
- <span data-ttu-id="fd0c8-124">Klasa: **SubscriptionAddons.cs**</span><span class="sxs-lookup"><span data-stu-id="fd0c8-124">Class: **SubscriptionAddons.cs**</span></span>

## <a name="rest-request"></a><span data-ttu-id="fd0c8-125">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="fd0c8-125">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="fd0c8-126">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="fd0c8-126">Request syntax</span></span>

| <span data-ttu-id="fd0c8-127">Metoda</span><span class="sxs-lookup"><span data-stu-id="fd0c8-127">Method</span></span>  | <span data-ttu-id="fd0c8-128">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="fd0c8-128">Request URI</span></span>                                                                                                                       |
|---------|-----------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="fd0c8-129">**Pobierz**</span><span class="sxs-lookup"><span data-stu-id="fd0c8-129">**GET**</span></span> | <span data-ttu-id="fd0c8-130">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/subscriptions/{id-for-subscription}/addons HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="fd0c8-130">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/subscriptions/{id-for-subscription}/addons HTTP/1.1</span></span> |

#### <a name="uri-parameter"></a><span data-ttu-id="fd0c8-131">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="fd0c8-131">URI parameter</span></span>

<span data-ttu-id="fd0c8-132">W tej tabeli wymieniono wymagane parametry zapytania w celu uzyskania listy dodatków dla subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="fd0c8-132">This table lists the required query parameters to get the list of add-ons for the subscription.</span></span>

| <span data-ttu-id="fd0c8-133">Nazwa</span><span class="sxs-lookup"><span data-stu-id="fd0c8-133">Name</span></span>                    | <span data-ttu-id="fd0c8-134">Typ</span><span class="sxs-lookup"><span data-stu-id="fd0c8-134">Type</span></span>     | <span data-ttu-id="fd0c8-135">Wymagane</span><span class="sxs-lookup"><span data-stu-id="fd0c8-135">Required</span></span> | <span data-ttu-id="fd0c8-136">Opis</span><span class="sxs-lookup"><span data-stu-id="fd0c8-136">Description</span></span>                               |
|-------------------------|----------|----------|-------------------------------------------|
| <span data-ttu-id="fd0c8-137">**identyfikator dzierżawy klienta**</span><span class="sxs-lookup"><span data-stu-id="fd0c8-137">**customer-tenant-id**</span></span>  | <span data-ttu-id="fd0c8-138">**guid**</span><span class="sxs-lookup"><span data-stu-id="fd0c8-138">**guid**</span></span> | <span data-ttu-id="fd0c8-139">Y</span><span class="sxs-lookup"><span data-stu-id="fd0c8-139">Y</span></span>        | <span data-ttu-id="fd0c8-140">Identyfikator GUID odpowiadający klientowi.</span><span class="sxs-lookup"><span data-stu-id="fd0c8-140">A GUID corresponding to the customer.</span></span>     |
| <span data-ttu-id="fd0c8-141">**id-for-subscription**</span><span class="sxs-lookup"><span data-stu-id="fd0c8-141">**id-for-subscription**</span></span> | <span data-ttu-id="fd0c8-142">**guid**</span><span class="sxs-lookup"><span data-stu-id="fd0c8-142">**guid**</span></span> | <span data-ttu-id="fd0c8-143">Y</span><span class="sxs-lookup"><span data-stu-id="fd0c8-143">Y</span></span>        | <span data-ttu-id="fd0c8-144">Identyfikator GUID odpowiadający subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="fd0c8-144">A GUID corresponding to the subscription.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="fd0c8-145">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="fd0c8-145">Request headers</span></span>

<span data-ttu-id="fd0c8-146">Aby uzyskać więcej informacji, [zobacz Partner Center REST headers (Nagłówki REST).](headers.md)</span><span class="sxs-lookup"><span data-stu-id="fd0c8-146">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="fd0c8-147">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="fd0c8-147">Request body</span></span>

<span data-ttu-id="fd0c8-148">Brak.</span><span class="sxs-lookup"><span data-stu-id="fd0c8-148">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="fd0c8-149">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="fd0c8-149">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/<customer-tenant-id>/subscriptions/<id-for-subscription>/addons HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 429902e2-ea2f-4704-b8a0-27fc53c539ba
MS-CorrelationId: c49004b1-224f-4d86-a607-6c8bcc52cfdd
```

## <a name="rest-response"></a><span data-ttu-id="fd0c8-150">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="fd0c8-150">REST response</span></span>

<span data-ttu-id="fd0c8-151">W przypadku powodzenia ta metoda zwraca kolekcję zasobów w treści odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="fd0c8-151">If successful, this method returns a collection of resources in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="fd0c8-152">Kody powodzenia i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="fd0c8-152">Response success and error codes</span></span>

<span data-ttu-id="fd0c8-153">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie, oraz dodatkowe informacje o debugowaniu.</span><span class="sxs-lookup"><span data-stu-id="fd0c8-153">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="fd0c8-154">Użyj narzędzia śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="fd0c8-154">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="fd0c8-155">Aby uzyskać pełną listę, zobacz [Kody błędów](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="fd0c8-155">For a full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="fd0c8-156">Przykład odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="fd0c8-156">Response example</span></span>

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
