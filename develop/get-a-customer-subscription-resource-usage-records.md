---
title: Pobieranie danych dotyczących użycia dla subskrypcji według zasobu
description: Zasobu ResourceUsageRecord można użyć do uzyskania rekordów użycia zasobów klienta dla określonych usług lub zasobów platformy Azure w bieżącym okresie rozliczeniowym.
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: e815430730dd7182380e9efd1fea80f9e84d2ce7
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/08/2020
ms.locfileid: "97767969"
---
# <a name="get-usage-data-for-subscription-by-resource"></a><span data-ttu-id="0d50a-103">Pobieranie danych dotyczących użycia dla subskrypcji według zasobu</span><span class="sxs-lookup"><span data-stu-id="0d50a-103">Get usage data for subscription by resource</span></span>

<span data-ttu-id="0d50a-104">**Dotyczy:**</span><span class="sxs-lookup"><span data-stu-id="0d50a-104">**Applies to:**</span></span>

- <span data-ttu-id="0d50a-105">Centrum partnerskie</span><span class="sxs-lookup"><span data-stu-id="0d50a-105">Partner Center</span></span>
- <span data-ttu-id="0d50a-106">Centrum partnerskie dla Microsoft Cloud Niemcy</span><span class="sxs-lookup"><span data-stu-id="0d50a-106">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="0d50a-107">Centrum partnerskie Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="0d50a-107">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="0d50a-108">W tym artykule opisano sposób pobierania zasobu **ResourceUsageRecord** .</span><span class="sxs-lookup"><span data-stu-id="0d50a-108">This article describes how to get the **ResourceUsageRecord** resource.</span></span> <span data-ttu-id="0d50a-109">Ten zasób reprezentuje zagregowaną sumę dla danego miesiąca dla poszczególnych zasobów zainicjowanych w planie platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="0d50a-109">This resource represents an aggregated total for the month for individual resources provisioned in your Azure plan.</span></span> <span data-ttu-id="0d50a-110">Za pomocą tego zasobu można pobrać rekordy użycia zasobów klienta dla określonych usług lub zasobów platformy Azure w bieżącym okresie rozliczeniowym.</span><span class="sxs-lookup"><span data-stu-id="0d50a-110">You can use this resource to get a customer's resource usage records for specific Azure services or resources during the current billing period.</span></span> <span data-ttu-id="0d50a-111">Ten interfejs API zwraca dane, które nie były wcześniej dostępne za pomocą interfejsów API wydatków platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="0d50a-111">This API returns data that was not available previously through Azure spending APIs.</span></span>

<span data-ttu-id="0d50a-112">*Ta trasa nie obsługuje subskrypcji Microsoft Azure (MS-AZR-0145P).*</span><span class="sxs-lookup"><span data-stu-id="0d50a-112">*This route does not support Microsoft Azure (MS-AZR-0145P) subscriptions.*</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0d50a-113">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="0d50a-113">Prerequisites</span></span>

- <span data-ttu-id="0d50a-114">Poświadczenia zgodnie z opisem w temacie [uwierzytelnianie w centrum partnerskim](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="0d50a-114">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="0d50a-115">Ten scenariusz obsługuje tylko uwierzytelnianie przy użyciu aplikacji i poświadczeń użytkownika.</span><span class="sxs-lookup"><span data-stu-id="0d50a-115">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="0d50a-116">Identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="0d50a-116">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="0d50a-117">Jeśli nie znasz identyfikatora klienta, możesz go wyszukać na [pulpicie nawigacyjnym](https://partner.microsoft.com/dashboard)Centrum partnerskiego.</span><span class="sxs-lookup"><span data-stu-id="0d50a-117">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="0d50a-118">Wybierz pozycję **dostawca CSP** z menu Centrum partnerskiego, po którym znajdują się **klienci**.</span><span class="sxs-lookup"><span data-stu-id="0d50a-118">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="0d50a-119">Wybierz klienta z listy klient, a następnie wybierz pozycję **konto**.</span><span class="sxs-lookup"><span data-stu-id="0d50a-119">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="0d50a-120">Na stronie konto klienta Znajdź **Identyfikator Microsoft** w sekcji **Informacje o koncie klienta** .</span><span class="sxs-lookup"><span data-stu-id="0d50a-120">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="0d50a-121">Identyfikator Microsoft jest taki sam jak identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="0d50a-121">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="0d50a-122">Identyfikator subskrypcji</span><span class="sxs-lookup"><span data-stu-id="0d50a-122">A subscription identifier</span></span>

## <a name="c"></a><span data-ttu-id="0d50a-123">C\#</span><span class="sxs-lookup"><span data-stu-id="0d50a-123">C\#</span></span>

<span data-ttu-id="0d50a-124">Aby uzyskać rekordy użycia zasobów klienta dla określonej usługi lub zasobu platformy Azure w bieżącym okresie rozliczeniowym:</span><span class="sxs-lookup"><span data-stu-id="0d50a-124">To get resource usage records of a customer for a specific Azure service or resource during the current billing period:</span></span>

1. <span data-ttu-id="0d50a-125">Użyj kolekcji **IAggregatePartner. Customers** , aby wywołać metodę **ById ()** .</span><span class="sxs-lookup"><span data-stu-id="0d50a-125">Use your **IAggregatePartner.Customers** collection to call the **ById()** method.</span></span>

2. <span data-ttu-id="0d50a-126">Wywołaj Właściwość subscriptions, a następnie **UsageRecords**, a następnie właściwości **resources** .</span><span class="sxs-lookup"><span data-stu-id="0d50a-126">Call the Subscriptions property, as well as **UsageRecords**, then the **Resources** property.</span></span> <span data-ttu-id="0d50a-127">Zakończ, wywołując metody get () lub GetAsync ().</span><span class="sxs-lookup"><span data-stu-id="0d50a-127">Finish by calling the Get() or GetAsync() methods.</span></span>

    ``` csharp
    // IAggregatePartner partnerOperations;
    // var selectedCustomerId as string;
    // var selectedSubscriptionId as string;

    var usageRecords = partnerOperations.Customers.ById(selectedCustomerId).Subscriptions.ById(selectedSubscriptionId).UsageRecords.Resources.Get();
    ```

<span data-ttu-id="0d50a-128">Aby zapoznać się z przykładem, zobacz następujące tematy:</span><span class="sxs-lookup"><span data-stu-id="0d50a-128">For an example, see the following:</span></span>

- <span data-ttu-id="0d50a-129">Przykład: [aplikacja testowa konsoli](console-test-app.md)</span><span class="sxs-lookup"><span data-stu-id="0d50a-129">Sample: [Console test app](console-test-app.md)</span></span>
- <span data-ttu-id="0d50a-130">Projekt: **PartnerSDK. FeatureSamples**</span><span class="sxs-lookup"><span data-stu-id="0d50a-130">Project: **PartnerSDK.FeatureSamples**</span></span>
- <span data-ttu-id="0d50a-131">Klasa: **GetSubscriptionUsageRecordsByResource.cs**</span><span class="sxs-lookup"><span data-stu-id="0d50a-131">Class: **GetSubscriptionUsageRecordsByResource.cs**</span></span>

## <a name="rest-request"></a><span data-ttu-id="0d50a-132">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="0d50a-132">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="0d50a-133">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="0d50a-133">Request syntax</span></span>

| <span data-ttu-id="0d50a-134">Metoda</span><span class="sxs-lookup"><span data-stu-id="0d50a-134">Method</span></span>  | <span data-ttu-id="0d50a-135">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="0d50a-135">Request URI</span></span>                                                                                                           |
|---------|-----------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="0d50a-136">**Pobierz**</span><span class="sxs-lookup"><span data-stu-id="0d50a-136">**GET**</span></span> | <span data-ttu-id="0d50a-137">[*{baseURL}*](partner-center-rest-urls.md)/V1/Customers/{Customer-tenant-ID}/subscriptions/{Subscription-ID}/resourceusagerecords http/1.1</span><span class="sxs-lookup"><span data-stu-id="0d50a-137">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/subscriptions/{subscription-id}/resourceusagerecords HTTP/1.1</span></span> |

#### <a name="uri-parameters"></a><span data-ttu-id="0d50a-138">Parametry identyfikatora URI</span><span class="sxs-lookup"><span data-stu-id="0d50a-138">URI parameters</span></span>

<span data-ttu-id="0d50a-139">Ta tabela zawiera listę wymaganych parametrów zapytania w celu uzyskania informacji o znamionowym użyciu klienta.</span><span class="sxs-lookup"><span data-stu-id="0d50a-139">This table lists the required query parameters to get the customer's rated usage information.</span></span>

| <span data-ttu-id="0d50a-140">Nazwa</span><span class="sxs-lookup"><span data-stu-id="0d50a-140">Name</span></span>                   | <span data-ttu-id="0d50a-141">Typ</span><span class="sxs-lookup"><span data-stu-id="0d50a-141">Type</span></span>     | <span data-ttu-id="0d50a-142">Wymagane</span><span class="sxs-lookup"><span data-stu-id="0d50a-142">Required</span></span> | <span data-ttu-id="0d50a-143">Opis</span><span class="sxs-lookup"><span data-stu-id="0d50a-143">Description</span></span>                               |
|------------------------|----------|----------|-------------------------------------------|
| <span data-ttu-id="0d50a-144">**Identyfikator dzierżawy klienta**</span><span class="sxs-lookup"><span data-stu-id="0d50a-144">**customer-tenant-id**</span></span> | <span data-ttu-id="0d50a-145">**guid**</span><span class="sxs-lookup"><span data-stu-id="0d50a-145">**guid**</span></span> | <span data-ttu-id="0d50a-146">Y</span><span class="sxs-lookup"><span data-stu-id="0d50a-146">Y</span></span>        | <span data-ttu-id="0d50a-147">Identyfikator GUID odpowiadający klientowi.</span><span class="sxs-lookup"><span data-stu-id="0d50a-147">A GUID corresponding to the customer.</span></span>     |
| <span data-ttu-id="0d50a-148">**Identyfikator subskrypcji**</span><span class="sxs-lookup"><span data-stu-id="0d50a-148">**subscription-id**</span></span>    | <span data-ttu-id="0d50a-149">**guid**</span><span class="sxs-lookup"><span data-stu-id="0d50a-149">**guid**</span></span> | <span data-ttu-id="0d50a-150">Y</span><span class="sxs-lookup"><span data-stu-id="0d50a-150">Y</span></span>        | <span data-ttu-id="0d50a-151">Identyfikator GUID odpowiadający identyfikatorowi [zasobu subskrypcji](subscription-resources.md#subscription)Centrum partnerskiego, który reprezentuje subskrypcję Microsoft Azure (MS-AZR-0145P) lub plan platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="0d50a-151">A GUID corresponding to the identifier of a Partner Center [subscription resource](subscription-resources.md#subscription), which represents a Microsoft Azure (MS-AZR-0145P) subscription or an Azure plan.</span></span> <span data-ttu-id="0d50a-152">*W przypadku zasobów subskrypcji planu platformy Azure Podaj **identyfikator planu** jako **Identyfikator subskrypcji** w tej trasie.*</span><span class="sxs-lookup"><span data-stu-id="0d50a-152">*For Azure plan subscription resources, provide the **plan-id** as the **subscription-id** in this route.*</span></span> |

### <a name="request-headers"></a><span data-ttu-id="0d50a-153">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="0d50a-153">Request headers</span></span>

<span data-ttu-id="0d50a-154">Aby uzyskać więcej informacji, zobacz [nagłówki REST Centrum partnerskiego](headers.md).</span><span class="sxs-lookup"><span data-stu-id="0d50a-154">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="0d50a-155">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="0d50a-155">Request body</span></span>

<span data-ttu-id="0d50a-156">Brak.</span><span class="sxs-lookup"><span data-stu-id="0d50a-156">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="0d50a-157">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="0d50a-157">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/{customer-tenant-id}/subscriptions/{subscription-id}/resourceusagerecords HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: e128c8e2-4c33-4940-a3e2-2e59b0abdc67
MS-CorrelationId: 47c36033-af5d-4457-80a4-512c1626fac4
```

## <a name="rest-response"></a><span data-ttu-id="0d50a-158">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="0d50a-158">REST response</span></span>

<span data-ttu-id="0d50a-159">Jeśli to się powiedzie, metoda zwraca zasób **PagedResourceCollection \<ResourceUsageRecord>** w treści odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="0d50a-159">If successful, this method returns a **PagedResourceCollection\<ResourceUsageRecord>** resource in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="0d50a-160">Kody sukcesu i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="0d50a-160">Response success and error codes</span></span>

<span data-ttu-id="0d50a-161">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie i dodatkowe informacje debugowania.</span><span class="sxs-lookup"><span data-stu-id="0d50a-161">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="0d50a-162">Użyj narzędzia do śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="0d50a-162">Use a network trace tool to read this code, the error type, and additional parameters.</span></span> <span data-ttu-id="0d50a-163">Aby uzyskać pełną listę, zobacz [kody błędów](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="0d50a-163">For a full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="0d50a-164">Przykład odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="0d50a-164">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 1120
Content-Type: application/json
MS-CorrelationId: 47c36033-af5d-4457-80a4-512c1626fac4
MS-RequestId: e128c8e2-4c33-4940-a3e2-2e59b0abdc67
Date: Tue, 17 Sep 2019 20:31:45 GMT

{
    "totalCount": 3,
    "items": [
        {
            "subscriptionId": "{subscription-id}",
            "resourceUri": "/subscriptions/{subscription-id}/resourceGroups/TESTRG1/providers/Microsoft.Compute/disks/testVM1_OsDisk_1_531d3c99534b4649ae025d485370143e",
            "resourceType": "Microsoft.Compute",
            "entitlementId": "{entitlemen-id}",
            "entitlementName": "Partner Subscription",
            "resourceGroupName": "TESTRG1",
            "name": "testVM1_OsDisk_1_531d3c99534b4649ae025d485370143e",
            "resourceName": "testVM1_OsDisk_1_531d3c99534b4649ae025d485370143e",
            "totalCost": 2.0211938955034572,
            "currencyCode": "GBP",
            "usdTotalCost": 2.4700000000000001,
            "lastModifiedDate": "2019-09-17T21:08:44.2566667+00:00",
            "attributes": {
                "objectType": "ResourceUsageRecord"
            }
        },
        {
            "subscriptionId": "{subscription-id}",
            "resourceUri": "/subscriptions/{subscription-id}/resourceGroups/TESTRG1/providers/Microsoft.Compute/virtualMachines/testVM1",
            "resourceType": "Microsoft.Compute",
            "entitlementId": "{entitlement-id}",
            "entitlementName": "Partner Subscription",
            "resourceGroupName": "TESTRG1",
            "name": "testVM1",
            "resourceName": "testVM1",
            "totalCost": 80.3322286322163563,
            "currencyCode": "GBP",
            "usdTotalCost": 98.1699999999999985,
            "lastModifiedDate": "2019-09-17T21:08:44.2566667+00:00",
            "attributes": {
                "objectType": "ResourceUsageRecord"
            }
        },
        {
            "subscriptionId": "{subscription-id}",
            "resourceUri": "/subscriptions/{subscription-id}/resourceGroups/testrg1/providers/Microsoft.Storage/storageAccounts/testrg1diag153",
            "resourceType": "Microsoft.Storage",
            "entitlementId": "{entitlemen-id}",
            "entitlementName": "Partner Subscription",
            "resourceGroupName": "testrg1",
            "name": "testrg1diag153",
            "resourceName": "testrg1diag153",
            "totalCost": 0.0081829712368561032,
            "currencyCode": "GBP",
            "usdTotalCost": 0.0099999999999999997,
            "lastModifiedDate": "2019-09-17T21:08:44.2566667+00:00",
            "attributes": {
                "objectType": "ResourceUsageRecord"
            }
        }
    ],
    "links": {
        "self": {
            "uri": "/customers/<customer-tenant-id>/subscriptions/<subscription-id>/resourceusagerecords",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "Collection"
    }
}
```
