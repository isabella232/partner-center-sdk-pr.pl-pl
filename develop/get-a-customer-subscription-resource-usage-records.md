---
title: Pobieranie danych dotyczących użycia dla subskrypcji według zasobu
description: Zasób ResourceUsageRecord umożliwia uzyskiwanie rekordów użycia zasobów klienta dla określonych usług lub zasobów platformy Azure w bieżącym okresie rozliczeniowym.
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 50edb9de1d09363b242c080a76c683732f05a5de
ms.sourcegitcommit: b1d6fd0ca93d8a3e30e970844d3164454415f553
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/09/2021
ms.locfileid: "111874843"
---
# <a name="get-usage-data-for-subscription-by-resource"></a><span data-ttu-id="25397-103">Pobieranie danych dotyczących użycia dla subskrypcji według zasobu</span><span class="sxs-lookup"><span data-stu-id="25397-103">Get usage data for subscription by resource</span></span>

<span data-ttu-id="25397-104">**Dotyczy:** Partner Center | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="25397-104">**Applies to**: Partner Center | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="25397-105">W tym artykule opisano sposób uzyskania **zasobu ResourceUsageRecord.**</span><span class="sxs-lookup"><span data-stu-id="25397-105">This article describes how to get the **ResourceUsageRecord** resource.</span></span> <span data-ttu-id="25397-106">Ten zasób reprezentuje zagregowaną sumę dla miesiąca dla poszczególnych zasobów aprowowanych w planie platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="25397-106">This resource represents an aggregated total for the month for individual resources provisioned in your Azure plan.</span></span> <span data-ttu-id="25397-107">Ten zasób umożliwia uzyskiwanie rekordów użycia zasobów klienta dla określonych usług lub zasobów platformy Azure w bieżącym okresie rozliczeniowym.</span><span class="sxs-lookup"><span data-stu-id="25397-107">You can use this resource to get a customer's resource usage records for specific Azure services or resources during the current billing period.</span></span> <span data-ttu-id="25397-108">Ten interfejs API zwraca dane, które nie były wcześniej dostępne za pośrednictwem interfejsów API wydatków platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="25397-108">This API returns data that was not available previously through Azure spending APIs.</span></span>

<span data-ttu-id="25397-109">*Ta trasa nie obsługuje Microsoft Azure subskrypcji (MS-AZR-0145P).*</span><span class="sxs-lookup"><span data-stu-id="25397-109">*This route does not support Microsoft Azure (MS-AZR-0145P) subscriptions.*</span></span>

## <a name="prerequisites"></a><span data-ttu-id="25397-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="25397-110">Prerequisites</span></span>

- <span data-ttu-id="25397-111">Poświadczenia zgodnie z opisem w te [Partner Center uwierzytelniania.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="25397-111">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="25397-112">Ten scenariusz obsługuje uwierzytelnianie tylko przy użyciu poświadczeń aplikacji i użytkownika.</span><span class="sxs-lookup"><span data-stu-id="25397-112">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="25397-113">Identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="25397-113">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="25397-114">Jeśli nie znasz identyfikatora klienta, możesz go znaleźć na pulpicie nawigacyjnym Partner Center [nawigacyjnym](https://partner.microsoft.com/dashboard).</span><span class="sxs-lookup"><span data-stu-id="25397-114">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="25397-115">Wybierz **pozycję CSP** z Partner Center menu, a następnie pozycję **Klienci.**</span><span class="sxs-lookup"><span data-stu-id="25397-115">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="25397-116">Wybierz klienta z listy klientów, a następnie wybierz pozycję **Konto**.</span><span class="sxs-lookup"><span data-stu-id="25397-116">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="25397-117">Na stronie Konto klienta odszukaj identyfikator **Microsoft w** **sekcji Informacje o koncie** klienta.</span><span class="sxs-lookup"><span data-stu-id="25397-117">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="25397-118">Identyfikator microsoft jest taki sam jak identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="25397-118">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="25397-119">Identyfikator subskrypcji</span><span class="sxs-lookup"><span data-stu-id="25397-119">A subscription identifier</span></span>

## <a name="c"></a><span data-ttu-id="25397-120">C\#</span><span class="sxs-lookup"><span data-stu-id="25397-120">C\#</span></span>

<span data-ttu-id="25397-121">Aby uzyskać rekordy użycia zasobów klienta dla określonej usługi lub zasobu platformy Azure w bieżącym okresie rozliczeniowym:</span><span class="sxs-lookup"><span data-stu-id="25397-121">To get resource usage records of a customer for a specific Azure service or resource during the current billing period:</span></span>

1. <span data-ttu-id="25397-122">Użyj **kolekcji IAggregatePartner.Customers,** aby wywołać **metodę ById().**</span><span class="sxs-lookup"><span data-stu-id="25397-122">Use your **IAggregatePartner.Customers** collection to call the **ById()** method.</span></span>

2. <span data-ttu-id="25397-123">Wywołaj właściwości Subscriptions i **UsageRecords**, a następnie **właściwość Resources.**</span><span class="sxs-lookup"><span data-stu-id="25397-123">Call the Subscriptions property and **UsageRecords**, and then the **Resources** property.</span></span> <span data-ttu-id="25397-124">Zakończ, wywołując metody Get() lub GetAsync().</span><span class="sxs-lookup"><span data-stu-id="25397-124">Finish by calling the Get() or GetAsync() methods.</span></span>

    ``` csharp
    // IAggregatePartner partnerOperations;
    // var selectedCustomerId as string;
    // var selectedSubscriptionId as string;

    var usageRecords = partnerOperations.Customers.ById(selectedCustomerId).Subscriptions.ById(selectedSubscriptionId).UsageRecords.Resources.Get();
    ```

<span data-ttu-id="25397-125">Przykład można znaleźć w następujących tematach:</span><span class="sxs-lookup"><span data-stu-id="25397-125">For an example, see the following:</span></span>

- <span data-ttu-id="25397-126">Przykład: [aplikacja testowa konsoli](console-test-app.md)</span><span class="sxs-lookup"><span data-stu-id="25397-126">Sample: [Console test app](console-test-app.md)</span></span>
- <span data-ttu-id="25397-127">Project: **PartnerSDK.FeatureSamples**</span><span class="sxs-lookup"><span data-stu-id="25397-127">Project: **PartnerSDK.FeatureSamples**</span></span>
- <span data-ttu-id="25397-128">Klasa: **GetSubscriptionUsageRecordsByResource.cs**</span><span class="sxs-lookup"><span data-stu-id="25397-128">Class: **GetSubscriptionUsageRecordsByResource.cs**</span></span>

## <a name="rest-request"></a><span data-ttu-id="25397-129">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="25397-129">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="25397-130">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="25397-130">Request syntax</span></span>

| <span data-ttu-id="25397-131">Metoda</span><span class="sxs-lookup"><span data-stu-id="25397-131">Method</span></span>  | <span data-ttu-id="25397-132">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="25397-132">Request URI</span></span>                                                                                                           |
|---------|-----------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="25397-133">**Pobierz**</span><span class="sxs-lookup"><span data-stu-id="25397-133">**GET**</span></span> | <span data-ttu-id="25397-134">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{identyfikator-dzierżawy-klienta}/subscriptions/{subscription-id}/resourceusagerecords HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="25397-134">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/subscriptions/{subscription-id}/resourceusagerecords HTTP/1.1</span></span> |

#### <a name="uri-parameters"></a><span data-ttu-id="25397-135">Parametry URI</span><span class="sxs-lookup"><span data-stu-id="25397-135">URI parameters</span></span>

<span data-ttu-id="25397-136">W tej tabeli wymieniono wymagane parametry zapytania w celu uzyskania informacji o użyciu ocenionym przez klienta.</span><span class="sxs-lookup"><span data-stu-id="25397-136">This table lists the required query parameters to get the customer's rated usage information.</span></span>

| <span data-ttu-id="25397-137">Nazwa</span><span class="sxs-lookup"><span data-stu-id="25397-137">Name</span></span>                   | <span data-ttu-id="25397-138">Typ</span><span class="sxs-lookup"><span data-stu-id="25397-138">Type</span></span>     | <span data-ttu-id="25397-139">Wymagane</span><span class="sxs-lookup"><span data-stu-id="25397-139">Required</span></span> | <span data-ttu-id="25397-140">Opis</span><span class="sxs-lookup"><span data-stu-id="25397-140">Description</span></span>                               |
|------------------------|----------|----------|-------------------------------------------|
| <span data-ttu-id="25397-141">**identyfikator dzierżawy klienta**</span><span class="sxs-lookup"><span data-stu-id="25397-141">**customer-tenant-id**</span></span> | <span data-ttu-id="25397-142">**guid**</span><span class="sxs-lookup"><span data-stu-id="25397-142">**guid**</span></span> | <span data-ttu-id="25397-143">Y</span><span class="sxs-lookup"><span data-stu-id="25397-143">Y</span></span>        | <span data-ttu-id="25397-144">Identyfikator GUID odpowiadający klientowi.</span><span class="sxs-lookup"><span data-stu-id="25397-144">A GUID corresponding to the customer.</span></span>     |
| <span data-ttu-id="25397-145">**subscription-id**</span><span class="sxs-lookup"><span data-stu-id="25397-145">**subscription-id**</span></span>    | <span data-ttu-id="25397-146">**guid**</span><span class="sxs-lookup"><span data-stu-id="25397-146">**guid**</span></span> | <span data-ttu-id="25397-147">Y</span><span class="sxs-lookup"><span data-stu-id="25397-147">Y</span></span>        | <span data-ttu-id="25397-148">Identyfikator GUID odpowiadający identyfikatorowi zasobu subskrypcji usługi [Partner Center,](subscription-resources.md#subscription)który reprezentuje subskrypcję Microsoft Azure (MS-AZR-0145P) lub plan platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="25397-148">A GUID corresponding to the identifier of a Partner Center [subscription resource](subscription-resources.md#subscription), which represents a Microsoft Azure (MS-AZR-0145P) subscription or an Azure plan.</span></span> <span data-ttu-id="25397-149">*W przypadku zasobów subskrypcji planu platformy Azure podaj **identyfikator planu** jako **subscription-id** w tej trasie.*</span><span class="sxs-lookup"><span data-stu-id="25397-149">*For Azure plan subscription resources, provide the **plan-id** as the **subscription-id** in this route.*</span></span> |

### <a name="request-headers"></a><span data-ttu-id="25397-150">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="25397-150">Request headers</span></span>

<span data-ttu-id="25397-151">Aby uzyskać więcej informacji, [zobacz Partner Center REST headers (Nagłówki REST).](headers.md)</span><span class="sxs-lookup"><span data-stu-id="25397-151">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="25397-152">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="25397-152">Request body</span></span>

<span data-ttu-id="25397-153">Brak.</span><span class="sxs-lookup"><span data-stu-id="25397-153">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="25397-154">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="25397-154">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/{customer-tenant-id}/subscriptions/{subscription-id}/resourceusagerecords HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: e128c8e2-4c33-4940-a3e2-2e59b0abdc67
MS-CorrelationId: 47c36033-af5d-4457-80a4-512c1626fac4
```

## <a name="rest-response"></a><span data-ttu-id="25397-155">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="25397-155">REST response</span></span>

<span data-ttu-id="25397-156">W przypadku powodzenia ta metoda zwraca **zasób \<ResourceUsageRecord> PagedResourceCollection** w treści odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="25397-156">If successful, this method returns a **PagedResourceCollection\<ResourceUsageRecord>** resource in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="25397-157">Kody powodzenia i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="25397-157">Response success and error codes</span></span>

<span data-ttu-id="25397-158">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie, oraz dodatkowe informacje o debugowaniu.</span><span class="sxs-lookup"><span data-stu-id="25397-158">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="25397-159">Użyj narzędzia śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="25397-159">Use a network trace tool to read this code, the error type, and additional parameters.</span></span> <span data-ttu-id="25397-160">Aby uzyskać pełną listę, zobacz [Kody błędów](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="25397-160">For a full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="25397-161">Przykład odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="25397-161">Response example</span></span>

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
