---
title: Pobierz wszystkie miesięczne rekordy użycia dla subskrypcji.
description: Możesz użyć kolekcji zasobów AzureResourceMonthlyUsageRecord, aby uzyskać listę usług w ramach subskrypcji klienta i ich skojarzone informacje o użyciu.
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: khpavan
ms.author: sakhanda
ms.openlocfilehash: 1dd09d4976c9626e088cda02ce36669dd7121a99
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/19/2020
ms.locfileid: "97768365"
---
# <a name="get-all-monthly-usage-records-for-a-subscription"></a><span data-ttu-id="9cf5c-103">Pobierz wszystkie miesięczne rekordy użycia dla subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="9cf5c-103">Get all monthly usage records for a subscription.</span></span>

<span data-ttu-id="9cf5c-104">**Dotyczy:**</span><span class="sxs-lookup"><span data-stu-id="9cf5c-104">**Applies to:**</span></span>

- <span data-ttu-id="9cf5c-105">Centrum partnerskie</span><span class="sxs-lookup"><span data-stu-id="9cf5c-105">Partner Center</span></span>
- <span data-ttu-id="9cf5c-106">Centrum partnerskie dla Microsoft Cloud Niemcy</span><span class="sxs-lookup"><span data-stu-id="9cf5c-106">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="9cf5c-107">Centrum partnerskie Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="9cf5c-107">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="9cf5c-108">Możesz użyć kolekcji zasobów [**AzureResourceMonthlyUsageRecord**](/dotnet/api/microsoft.store.partnercenter.models.usage.azureresourcemonthlyusagerecord) , aby uzyskać listę usług w ramach subskrypcji klienta i ich skojarzone informacje o użyciu.</span><span class="sxs-lookup"><span data-stu-id="9cf5c-108">You can use the [**AzureResourceMonthlyUsageRecord**](/dotnet/api/microsoft.store.partnercenter.models.usage.azureresourcemonthlyusagerecord) resource collection to get a list of services within a customer's subscription and their associated rated usage information.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9cf5c-109">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="9cf5c-109">Prerequisites</span></span>

- <span data-ttu-id="9cf5c-110">Poświadczenia zgodnie z opisem w temacie [uwierzytelnianie w centrum partnerskim](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="9cf5c-110">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="9cf5c-111">Ten scenariusz obsługuje uwierzytelnianie zarówno w przypadku aplikacji autonomicznych, jak i aplikacji oraz poświadczeń użytkownika.</span><span class="sxs-lookup"><span data-stu-id="9cf5c-111">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="9cf5c-112">Identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="9cf5c-112">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="9cf5c-113">Jeśli nie znasz identyfikatora klienta, możesz go wyszukać na [pulpicie nawigacyjnym](https://partner.microsoft.com/dashboard)Centrum partnerskiego.</span><span class="sxs-lookup"><span data-stu-id="9cf5c-113">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="9cf5c-114">Wybierz pozycję **dostawca CSP** z menu Centrum partnerskiego, po którym znajdują się **klienci**.</span><span class="sxs-lookup"><span data-stu-id="9cf5c-114">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="9cf5c-115">Wybierz klienta z listy klient, a następnie wybierz pozycję **konto**.</span><span class="sxs-lookup"><span data-stu-id="9cf5c-115">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="9cf5c-116">Na stronie konto klienta Znajdź **Identyfikator Microsoft** w sekcji **Informacje o koncie klienta** .</span><span class="sxs-lookup"><span data-stu-id="9cf5c-116">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="9cf5c-117">Identyfikator Microsoft jest taki sam jak identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="9cf5c-117">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="9cf5c-118">Identyfikator subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="9cf5c-118">A subscription identifier.</span></span>

<span data-ttu-id="9cf5c-119">*Ten interfejs API obsługuje tylko subskrypcje Microsoft Azure (MS-AZR-0145P). Jeśli używasz planu platformy Azure, zobacz [pobieranie danych użycia dla subskrypcji według miernika](get-a-customer-subscription-meter-usage-records.md) .*</span><span class="sxs-lookup"><span data-stu-id="9cf5c-119">*This API only supports Microsoft Azure (MS-AZR-0145P) subscriptions. If you are using an Azure plan, see [Get usage data for subscription by meter](get-a-customer-subscription-meter-usage-records.md) instead.*</span></span>

## <a name="c"></a><span data-ttu-id="9cf5c-120">C\#</span><span class="sxs-lookup"><span data-stu-id="9cf5c-120">C\#</span></span>

<span data-ttu-id="9cf5c-121">Aby uzyskać informacje o użyciu zasobów subskrypcji:</span><span class="sxs-lookup"><span data-stu-id="9cf5c-121">To get a subscription's resource usage information:</span></span>

1. <span data-ttu-id="9cf5c-122">Użyj kolekcji **IAggregatePartner. Customers** , aby wywołać metodę **ById ()** .</span><span class="sxs-lookup"><span data-stu-id="9cf5c-122">Use your **IAggregatePartner.Customers** collection to call the **ById()** method.</span></span>

2. <span data-ttu-id="9cf5c-123">Wywołaj Właściwość **subscriptions** , a następnie **UsageRecords**, a następnie właściwości **resources** .</span><span class="sxs-lookup"><span data-stu-id="9cf5c-123">Call the **Subscriptions** property, as well as **UsageRecords**, then the **Resources** property.</span></span>
3. <span data-ttu-id="9cf5c-124">Wywołaj metody **Get ()** lub **GetAsync ()** .</span><span class="sxs-lookup"><span data-stu-id="9cf5c-124">Call the **Get()** or **GetAsync()** methods.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// var selectedCustomerId as string;
// var selectedSubscriptionID as string;

var usageRecords = partnerOperations.Customers.ById(selectedCustomerId).Subscriptions.ById(selectedSubscriptionId).UsageRecords.Resources.Get();
```

<span data-ttu-id="9cf5c-125">Aby zapoznać się z przykładem, zobacz następujące tematy:</span><span class="sxs-lookup"><span data-stu-id="9cf5c-125">For an example, see the following:</span></span>

- <span data-ttu-id="9cf5c-126">Przykład: [aplikacja testowa konsoli](console-test-app.md)</span><span class="sxs-lookup"><span data-stu-id="9cf5c-126">Sample: [Console test app](console-test-app.md)</span></span>
- <span data-ttu-id="9cf5c-127">Projekt: **PartnerSDK. FeatureSample**</span><span class="sxs-lookup"><span data-stu-id="9cf5c-127">Project: **PartnerSDK.FeatureSample**</span></span>
- <span data-ttu-id="9cf5c-128">Klasa: **SubscriptionResourceUsageRecords.cs**</span><span class="sxs-lookup"><span data-stu-id="9cf5c-128">Class: **SubscriptionResourceUsageRecords.cs**</span></span>

## <a name="rest-request"></a><span data-ttu-id="9cf5c-129">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="9cf5c-129">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="9cf5c-130">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="9cf5c-130">Request syntax</span></span>

| <span data-ttu-id="9cf5c-131">Metoda</span><span class="sxs-lookup"><span data-stu-id="9cf5c-131">Method</span></span>  | <span data-ttu-id="9cf5c-132">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="9cf5c-132">Request URI</span></span>                                                                                                                                       |
|---------|---------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="9cf5c-133">**Pobierz**</span><span class="sxs-lookup"><span data-stu-id="9cf5c-133">**GET**</span></span> | <span data-ttu-id="9cf5c-134">[*{baseURL}*](partner-center-rest-urls.md)/V1/Customers/{Customer-tenant-ID}/subscriptions/{ID-for-Subscription}/usagerecords/Resources http/1.1</span><span class="sxs-lookup"><span data-stu-id="9cf5c-134">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/subscriptions/{id-for-subscription}/usagerecords/resources HTTP/1.1</span></span> |

#### <a name="uri-parameters"></a><span data-ttu-id="9cf5c-135">Parametry identyfikatora URI</span><span class="sxs-lookup"><span data-stu-id="9cf5c-135">URI parameters</span></span>

<span data-ttu-id="9cf5c-136">Ta tabela zawiera listę wymaganych parametrów zapytania, aby uzyskać informacje o ocenach użycia.</span><span class="sxs-lookup"><span data-stu-id="9cf5c-136">This table lists the required query parameters to get the rated usage information.</span></span>

| <span data-ttu-id="9cf5c-137">Nazwa</span><span class="sxs-lookup"><span data-stu-id="9cf5c-137">Name</span></span>                    | <span data-ttu-id="9cf5c-138">Typ</span><span class="sxs-lookup"><span data-stu-id="9cf5c-138">Type</span></span>     | <span data-ttu-id="9cf5c-139">Wymagane</span><span class="sxs-lookup"><span data-stu-id="9cf5c-139">Required</span></span> | <span data-ttu-id="9cf5c-140">Opis</span><span class="sxs-lookup"><span data-stu-id="9cf5c-140">Description</span></span>                               |
|-------------------------|----------|----------|-------------------------------------------|
| <span data-ttu-id="9cf5c-141">**Identyfikator dzierżawy klienta**</span><span class="sxs-lookup"><span data-stu-id="9cf5c-141">**customer-tenant-id**</span></span>  | <span data-ttu-id="9cf5c-142">**guid**</span><span class="sxs-lookup"><span data-stu-id="9cf5c-142">**guid**</span></span> | <span data-ttu-id="9cf5c-143">Y</span><span class="sxs-lookup"><span data-stu-id="9cf5c-143">Y</span></span>        | <span data-ttu-id="9cf5c-144">Identyfikator GUID odpowiadający klientowi.</span><span class="sxs-lookup"><span data-stu-id="9cf5c-144">A GUID corresponding to the customer.</span></span>     |
| <span data-ttu-id="9cf5c-145">**Identyfikator subskrypcji**</span><span class="sxs-lookup"><span data-stu-id="9cf5c-145">**subscription-id**</span></span> | <span data-ttu-id="9cf5c-146">**guid**</span><span class="sxs-lookup"><span data-stu-id="9cf5c-146">**guid**</span></span> | <span data-ttu-id="9cf5c-147">Y</span><span class="sxs-lookup"><span data-stu-id="9cf5c-147">Y</span></span>        | <span data-ttu-id="9cf5c-148">Identyfikator GUID odpowiadający subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="9cf5c-148">A GUID corresponding to the subscription.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="9cf5c-149">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="9cf5c-149">Request headers</span></span>

<span data-ttu-id="9cf5c-150">Aby uzyskać więcej informacji, zobacz [nagłówki REST Centrum partnerskiego](headers.md).</span><span class="sxs-lookup"><span data-stu-id="9cf5c-150">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="9cf5c-151">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="9cf5c-151">Request body</span></span>

<span data-ttu-id="9cf5c-152">Brak.</span><span class="sxs-lookup"><span data-stu-id="9cf5c-152">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="9cf5c-153">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="9cf5c-153">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/{customer-tenant-id}/subscriptions/{id-for-subscription}/usagerecords/resources HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 65b26053-37d0-4303-9fd1-46ad8012bcb6
MS-CorrelationId: 47c36033-af5d-4457-80a4-512c1626fac4
```

## <a name="rest-response"></a><span data-ttu-id="9cf5c-154">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="9cf5c-154">REST response</span></span>

<span data-ttu-id="9cf5c-155">Jeśli to się powiedzie, ta metoda zwraca kolekcję zasobów **AzureResourceMonthlyUsageRecord** w treści odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="9cf5c-155">If successful, this method returns a collection of **AzureResourceMonthlyUsageRecord** resources in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="9cf5c-156">Kody sukcesu i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="9cf5c-156">Response success and error codes</span></span>

<span data-ttu-id="9cf5c-157">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie i dodatkowe informacje debugowania.</span><span class="sxs-lookup"><span data-stu-id="9cf5c-157">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="9cf5c-158">Użyj narzędzia do śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="9cf5c-158">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="9cf5c-159">Aby uzyskać pełną listę, zobacz [kody błędów](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="9cf5c-159">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="9cf5c-160">Przykład odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="9cf5c-160">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 12014
Content-Type: application/json
MS-CorrelationId: 648a26a4-a63e-459f-844b-4f29d7913353
MS-RequestId: be82a8ba-4a53-49f7-8313-b033c058687e
Date: Tue, 10 Nov 2015 19:09:59 GMT

{
    "totalCount":20,
    "items":[{
        "category":"Storage",
        "subcategory":"LOCALLY REDUNDANT",
        "quantityUsed":0.151287527825352,
        "unit":"GB",
        "id":"2a2419c0-cefe-46b2-8004-8eb002ad606c",
        "name":"Azure Resource 1",
        "totalCost":0.195779159290613,
        "currencyLocale":"en-US",
        "attributes":{
            "objectType":"AzureResourceMonthlyUsageRecord"
        }
    },
    {
        "category":"Remote App",
        "subcategory":"Remote App",
        "quantityUsed":0.932546524299563,
        "unit":"GB",
        "id":"7e4099c8-2b3d-41a6-a1bd-d5cf315989b2",
        "name":"Azure Resource 2",
        "totalCost":0.920983775016379,
        "currencyLocale":"en-US",
        "attributes":{
            "objectType":"AzureResourceMonthlyUsageRecord"
        }
    }],
    "links":{
        "self":{
            "uri":"/v1/customers/<customer-tenant-id>/subscriptions/<id-for-subscription>%20/usagerecords",
            "method":"GET",
            "headers":[]
        }
    },
    "attributes":{
        "objectType":"Collection"
    }
}
```
