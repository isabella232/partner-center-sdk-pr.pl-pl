---
title: Pobieranie danych dotyczących użycia dla subskrypcji według miernika
description: Kolekcji zasobów MeterUsageRecord można użyć do uzyskania rekordów użycia zliczania klienta dla określonych usług lub zasobów platformy Azure w bieżącym okresie rozliczeniowym.
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: df981eae8d2caee2dcb7f36696725ec011ead75b
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/08/2020
ms.locfileid: "97767973"
---
# <a name="get-usage-data-for-subscription-by-meter"></a><span data-ttu-id="6d574-103">Pobieranie danych dotyczących użycia dla subskrypcji według miernika</span><span class="sxs-lookup"><span data-stu-id="6d574-103">Get usage data for subscription by meter</span></span>

<span data-ttu-id="6d574-104">**Dotyczy:**</span><span class="sxs-lookup"><span data-stu-id="6d574-104">**Applies to:**</span></span>

- <span data-ttu-id="6d574-105">Centrum partnerskie</span><span class="sxs-lookup"><span data-stu-id="6d574-105">Partner Center</span></span>
- <span data-ttu-id="6d574-106">Centrum partnerskie dla Microsoft Cloud Niemcy</span><span class="sxs-lookup"><span data-stu-id="6d574-106">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="6d574-107">Centrum partnerskie Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="6d574-107">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="6d574-108">Kolekcji zasobów **MeterUsageRecord** można użyć do uzyskania rekordów użycia zliczania klienta dla określonych usług lub zasobów platformy Azure w bieżącym okresie rozliczeniowym.</span><span class="sxs-lookup"><span data-stu-id="6d574-108">You can use the **MeterUsageRecord** resource collection to get meter usage records of a customer for specific Azure services or resources during the current billing period.</span></span> <span data-ttu-id="6d574-109">Ta kolekcja zasobów reprezentuje zagregowaną sumę dla każdego licznika dla bieżącego cyklu rozliczeniowego w całym planie platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="6d574-109">This resource collection represents an aggregated total for each meter for the current billing cycle, across your entire Azure plan.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6d574-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="6d574-110">Prerequisites</span></span>

- <span data-ttu-id="6d574-111">Poświadczenia zgodnie z opisem w temacie [uwierzytelnianie w centrum partnerskim](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="6d574-111">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="6d574-112">Ten scenariusz obsługuje tylko uwierzytelnianie przy użyciu aplikacji i poświadczeń użytkownika.</span><span class="sxs-lookup"><span data-stu-id="6d574-112">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="6d574-113">Identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="6d574-113">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="6d574-114">Jeśli nie znasz identyfikatora klienta, możesz go wyszukać na [pulpicie nawigacyjnym](https://partner.microsoft.com/dashboard)Centrum partnerskiego.</span><span class="sxs-lookup"><span data-stu-id="6d574-114">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="6d574-115">Wybierz pozycję **dostawca CSP** z menu Centrum partnerskiego, po którym znajdują się **klienci**.</span><span class="sxs-lookup"><span data-stu-id="6d574-115">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="6d574-116">Wybierz klienta z listy klient, a następnie wybierz pozycję **konto**.</span><span class="sxs-lookup"><span data-stu-id="6d574-116">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="6d574-117">Na stronie konto klienta Znajdź **Identyfikator Microsoft** w sekcji **Informacje o koncie klienta** .</span><span class="sxs-lookup"><span data-stu-id="6d574-117">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="6d574-118">Identyfikator Microsoft jest taki sam jak identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="6d574-118">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="6d574-119">Identyfikator subskrypcji</span><span class="sxs-lookup"><span data-stu-id="6d574-119">A subscription ID</span></span>

<span data-ttu-id="6d574-120">*Ta nowa trasa jest równoznaczna z `subscriptions/{subscription-id}/usagerecords/resources` , która będzie nadal działać tylko w przypadku subskrypcji Microsoft Azure (MS-AZR-0145P).*</span><span class="sxs-lookup"><span data-stu-id="6d574-120">*This new route is equivalent to `subscriptions/{subscription-id}/usagerecords/resources`, which will continue to function only for Microsoft Azure (MS-AZR-0145P) subscriptions.*</span></span> <span data-ttu-id="6d574-121">Ta nowa trasa będzie obsługiwać zarówno subskrypcje Microsoft Azure (MS-AZR-0145P), jak i plany platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="6d574-121">This new route will support both Microsoft Azure (MS-AZR-0145P) subscriptions and Azure plans.</span></span> <span data-ttu-id="6d574-122">Aby uzyskać informacje dotyczące planu platformy Azure, musisz przełączyć się do tej nowej trasy.</span><span class="sxs-lookup"><span data-stu-id="6d574-122">In order to get this information for your Azure plan, you need to switch to this new route.</span></span> <span data-ttu-id="6d574-123">Poza właściwościami wymienionymi w poniższych sekcjach odpowiedź jest taka sama jak w przypadku starej trasy.</span><span class="sxs-lookup"><span data-stu-id="6d574-123">Other than the properties mentioned in the following sections, the response is the same as the old route.</span></span>

## <a name="c"></a><span data-ttu-id="6d574-124">C\#</span><span class="sxs-lookup"><span data-stu-id="6d574-124">C\#</span></span>

<span data-ttu-id="6d574-125">Aby uzyskać rekordy użycia liczników klienta dla określonej usługi lub zasobu platformy Azure w bieżącym okresie rozliczeniowym:</span><span class="sxs-lookup"><span data-stu-id="6d574-125">To get meter usage records of a customer for a specific Azure service or resource during the current billing period:</span></span>

1. <span data-ttu-id="6d574-126">Użyj kolekcji **IAggregatePartner. Customers** , aby wywołać metodę **ById ()** .</span><span class="sxs-lookup"><span data-stu-id="6d574-126">Use your **IAggregatePartner.Customers** collection to call the **ById()** method.</span></span>

2. <span data-ttu-id="6d574-127">Wywołaj Właściwość subscriptions i **UsageRecords**, a następnie właściwość **mierników** .</span><span class="sxs-lookup"><span data-stu-id="6d574-127">Call the Subscriptions property, and **UsageRecords**, then the **Meters** property.</span></span> <span data-ttu-id="6d574-128">Zakończ, wywołując metody get () lub GetAsync ().</span><span class="sxs-lookup"><span data-stu-id="6d574-128">Finish by calling the Get() or GetAsync() methods.</span></span>

    ``` csharp
    // IAggregatePartner partnerOperations;
    // var selectedCustomerId as string;
    // var selectedSubscriptionId as string;

    var usageRecords = partnerOperations.Customers.ById(selectedCustomerId).Subscriptions.ById(selectedSubscriptionId).UsageRecords.Meters.Get();
    ```

<span data-ttu-id="6d574-129">Aby zapoznać się z przykładem, zobacz następujący przykład:</span><span class="sxs-lookup"><span data-stu-id="6d574-129">For an example, see the following sample:</span></span>

- <span data-ttu-id="6d574-130">Przykład: [aplikacja testowa konsoli](console-test-app.md)</span><span class="sxs-lookup"><span data-stu-id="6d574-130">Sample: [Console test app](console-test-app.md)</span></span>
- <span data-ttu-id="6d574-131">Projekt: **PartnerSDK. FeatureSamples**</span><span class="sxs-lookup"><span data-stu-id="6d574-131">Project: **PartnerSDK.FeatureSamples**</span></span>
- <span data-ttu-id="6d574-132">Klasa: **GetSubscriptionUsageRecordsByMeter.cs**</span><span class="sxs-lookup"><span data-stu-id="6d574-132">Class: **GetSubscriptionUsageRecordsByMeter.cs**</span></span>

## <a name="rest-request"></a><span data-ttu-id="6d574-133">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="6d574-133">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="6d574-134">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="6d574-134">Request syntax</span></span>

| <span data-ttu-id="6d574-135">Metoda</span><span class="sxs-lookup"><span data-stu-id="6d574-135">Method</span></span>  | <span data-ttu-id="6d574-136">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="6d574-136">Request URI</span></span>                                                                                                                             |
|---------|-----------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="6d574-137">**Pobierz**</span><span class="sxs-lookup"><span data-stu-id="6d574-137">**GET**</span></span> | <span data-ttu-id="6d574-138">[*{baseURL}*](partner-center-rest-urls.md)/V1/Customers/{Customer-tenant-ID}/subscriptions/{Subscription-ID}/meterusagerecords http/1.1</span><span class="sxs-lookup"><span data-stu-id="6d574-138">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/subscriptions/{subscription-id}/meterusagerecords HTTP/1.1</span></span> |

#### <a name="uri-parameters"></a><span data-ttu-id="6d574-139">Parametry identyfikatora URI</span><span class="sxs-lookup"><span data-stu-id="6d574-139">URI parameters</span></span>

<span data-ttu-id="6d574-140">Ta tabela zawiera listę wymaganych parametrów zapytania w celu uzyskania informacji o znamionowym użyciu klienta.</span><span class="sxs-lookup"><span data-stu-id="6d574-140">This table lists the required query parameters to get the customer's rated usage information.</span></span>

| <span data-ttu-id="6d574-141">Nazwa</span><span class="sxs-lookup"><span data-stu-id="6d574-141">Name</span></span>                   | <span data-ttu-id="6d574-142">Typ</span><span class="sxs-lookup"><span data-stu-id="6d574-142">Type</span></span>     | <span data-ttu-id="6d574-143">Wymagane</span><span class="sxs-lookup"><span data-stu-id="6d574-143">Required</span></span> | <span data-ttu-id="6d574-144">Opis</span><span class="sxs-lookup"><span data-stu-id="6d574-144">Description</span></span>                               |
|------------------------|----------|----------|-------------------------------------------|
| <span data-ttu-id="6d574-145">**Identyfikator dzierżawy klienta**</span><span class="sxs-lookup"><span data-stu-id="6d574-145">**customer-tenant-id**</span></span> | <span data-ttu-id="6d574-146">**guid**</span><span class="sxs-lookup"><span data-stu-id="6d574-146">**guid**</span></span> | <span data-ttu-id="6d574-147">Y</span><span class="sxs-lookup"><span data-stu-id="6d574-147">Y</span></span>        | <span data-ttu-id="6d574-148">Identyfikator GUID odpowiadający klientowi.</span><span class="sxs-lookup"><span data-stu-id="6d574-148">A GUID corresponding to the customer.</span></span>     |
| <span data-ttu-id="6d574-149">**Identyfikator subskrypcji**</span><span class="sxs-lookup"><span data-stu-id="6d574-149">**subscription-id**</span></span>    | <span data-ttu-id="6d574-150">**guid**</span><span class="sxs-lookup"><span data-stu-id="6d574-150">**guid**</span></span> | <span data-ttu-id="6d574-151">Y</span><span class="sxs-lookup"><span data-stu-id="6d574-151">Y</span></span>        | <span data-ttu-id="6d574-152">Identyfikator GUID odpowiadający identyfikatorowi [zasobu subskrypcji](subscription-resources.md#subscription)Centrum partnerskiego, który reprezentuje subskrypcję Microsoft Azure (MS-AZR-0145P) lub plan platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="6d574-152">A GUID corresponding to the identifier of a Partner Center [subscription resource](subscription-resources.md#subscription), which represents a Microsoft Azure (MS-AZR-0145P) subscription or an Azure plan.</span></span> <span data-ttu-id="6d574-153">*W przypadku zasobów subskrypcji planu platformy Azure Podaj **identyfikator planu** jako **Identyfikator subskrypcji** w tej trasie.*</span><span class="sxs-lookup"><span data-stu-id="6d574-153">*For Azure plan subscription resources, provide the **plan-id** as the **subscription-id** in this route.*</span></span> |

### <a name="request-headers"></a><span data-ttu-id="6d574-154">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="6d574-154">Request headers</span></span>

<span data-ttu-id="6d574-155">Aby uzyskać więcej informacji, zobacz [nagłówki REST Centrum partnerskiego](headers.md).</span><span class="sxs-lookup"><span data-stu-id="6d574-155">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="6d574-156">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="6d574-156">Request body</span></span>

<span data-ttu-id="6d574-157">Brak.</span><span class="sxs-lookup"><span data-stu-id="6d574-157">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="6d574-158">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="6d574-158">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/{customer-tenant-id}/subscriptions/{subscription-id}/meterusagerecords HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: e128c8e2-4c33-4940-a3e2-2e59b0abdc67
MS-CorrelationId: 47c36033-af5d-4457-80a4-512c1626fac4
```

## <a name="rest-response"></a><span data-ttu-id="6d574-159">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="6d574-159">REST response</span></span>

<span data-ttu-id="6d574-160">Jeśli to się powiedzie, metoda zwraca zasób **PagedResourceCollection \<MeterUsageRecord>** w treści odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="6d574-160">If successful, this method returns a **PagedResourceCollection\<MeterUsageRecord>** resource in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="6d574-161">Kody sukcesu i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="6d574-161">Response success and error codes</span></span>

<span data-ttu-id="6d574-162">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie i dodatkowe informacje debugowania.</span><span class="sxs-lookup"><span data-stu-id="6d574-162">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="6d574-163">Użyj narzędzia do śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="6d574-163">Use a network trace tool to read this code, the error type, and additional parameters.</span></span> <span data-ttu-id="6d574-164">Aby uzyskać pełną listę, zobacz [kody błędów](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="6d574-164">For a full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example-for-microsoft-azure-ms-azr-0145p-subscriptions"></a><span data-ttu-id="6d574-165">Przykład odpowiedzi dla subskrypcji Microsoft Azure (MS-AZR-0145P)</span><span class="sxs-lookup"><span data-stu-id="6d574-165">Response example for Microsoft Azure (MS-AZR-0145P) subscriptions</span></span>

<span data-ttu-id="6d574-166">W tym przykładzie klient zakupił **145Pą usługę Azure PayG**.</span><span class="sxs-lookup"><span data-stu-id="6d574-166">In this example, the customer purchased **145P Azure PayG**.</span></span>

<span data-ttu-id="6d574-167">*W przypadku klientów z subskrypcją usługi Microsoft Azure (MS-AZR-0145P) nie zostanie zmieniona odpowiedź interfejsu API.*</span><span class="sxs-lookup"><span data-stu-id="6d574-167">*For customers with a Microsoft Azure (MS-AZR-0145P) subscription, there will be no change to API response.*</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 1120
Content-Type: application/json
MS-CorrelationId: 47c36033-af5d-4457-80a4-512c1626fac4
MS-RequestId: e128c8e2-4c33-4940-a3e2-2e59b0abdc67
Date: Tue, 17 Sep 2019 20:31:45 GMT

{
    "totalCount": 1,
    "items": [
        {
            "status": "active",
            "offerId": "MS-AZR-0145P",
            "resourceId": "11111111-F347-41B6-B02C-187B1B778A43",
            "id": "11111111-F347-41B6-B02C-187B1B778A43",
            "resourceName": "Microsoft Azure",
            "name": "Microsoft Azure",
            "totalCost": 22.861172,
            "currencyLocale": "fr-FR",
            "usdTotalCost": 0,
            "lastModifiedDate": "2019-09-01T23:04:41.193+00:00",
            "attributes": {
                "objectType": "SubscriptionMonthlyUsageRecord"
            }
        }
    ],
    "links": {
        "self": {
            "uri": "/customers/{customer-tenant-id}/subscriptions/usagerecords/",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "Collection"
    }
}
```

## <a name="rest-response-example-for-azure-plan"></a><span data-ttu-id="6d574-168">Przykład odpowiedzi REST dla usługi Azure plan</span><span class="sxs-lookup"><span data-stu-id="6d574-168">REST response example for Azure plan</span></span>

<span data-ttu-id="6d574-169">W tym przykładzie klient kupił plan platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="6d574-169">In this example, the customer purchased an Azure plan.</span></span>

<span data-ttu-id="6d574-170">*W przypadku klientów z planami platformy Azure w odpowiedzi interfejsu API istnieją następujące zmiany:*</span><span class="sxs-lookup"><span data-stu-id="6d574-170">*For customers with Azure plans, there are the following changes in the API response:*</span></span>

- <span data-ttu-id="6d574-171">**currencyLocale** został zastąpiony **CurrencyCode**</span><span class="sxs-lookup"><span data-stu-id="6d574-171">**currencyLocale** is replaced with **currencyCode**</span></span>
- <span data-ttu-id="6d574-172">**usdTotalCost** jest nowym polem</span><span class="sxs-lookup"><span data-stu-id="6d574-172">**usdTotalCost** is a new field</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 1120
Content-Type: application/json
MS-CorrelationId: 47c36033-af5d-4457-80a4-512c1626fac4
MS-RequestId: e128c8e2-4c33-4940-a3e2-2e59b0abdc67
Date: Fri, 26 Feb 2016 20:31:45 GMT

{
    "totalCount": 4,
    "items": [
        {
            "subscriptionId": "{subscription-id}",
            "meterId": "DZH318Z0BNVX-005J-Data Transfer In (GB)",
            "meterName": "Data Transfer In",
            "category": "Bandwidth",
            "subcategory": "Bandwidth",
            "quantityUsed": 0.01129,
            "unit": "1 GB",
            "totalCost": 0,
            "currencyCode": "GBP",
            "usdTotalCost": 0,
            "lastModifiedDate": "2019-09-17T21:08:44.2566667+00:00",
            "attributes": {
                "objectType": "MeterUsageRecord"
            }
        },
        {
            "subscriptionId": "{subscription-id}",
            "meterId": "DZH318Z0BNVX-005J-Data Transfer Out (GB)",
            "meterName": "Data Transfer Out",
            "category": "Bandwidth",
            "subcategory": "Bandwidth",
            "quantityUsed": 0.000224,
            "unit": "1 GB",
            "totalCost": 0,
            "currencyCode": "GBP",
            "usdTotalCost": 0,
            "lastModifiedDate": "2019-09-17T21:08:44.2566667+00:00",
            "attributes": {
                "objectType": "MeterUsageRecord"
            }
        },
        {
            "subscriptionId": "{subscription-id}",
            "meterId": "DZH318Z0BNZ5-006G-10K Batch Write Operations",
            "meterName": "Batch Write Operations",
            "category": "Storage",
            "subcategory": "Tables",
            "quantityUsed": 0.2462,
            "unit": "10K",
            "totalCost": 0,
            "currencyCode": "GBP",
            "usdTotalCost": 0,
            "lastModifiedDate": "2019-09-17T21:08:44.2566667+00:00",
            "attributes": {
                "objectType": "MeterUsageRecord"
            }
        },
        {
            "subscriptionId": "{subscription-id}",
            "meterId": "DZH318Z0BNZ5-006G-Data Stored (GB/Month)",
            "meterName": "LRS Data Stored",
            "category": "Storage",
            "subcategory": "Tables",
            "quantityUsed": 0.002632,
            "unit": "1 GB/Month",
            "totalCost": 0,
            "currencyCode": "GBP",
            "usdTotalCost": 0,
            "lastModifiedDate": "2019-09-17T21:08:44.2566667+00:00",
            "attributes": {
                "objectType": "MeterUsageRecord"
            }
        }
    ],
    "links": {
        "self": {
            "uri": "/customers/<customer-tenant-id>/subscriptions/<subscription-id>/meterusagerecords",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "Collection"
    }
}
```
