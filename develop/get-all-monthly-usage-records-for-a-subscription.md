---
title: Pobieranie wszystkich rekordów dotyczących miesięcznego użycia dla subskrypcji
description: Możesz użyć kolekcji zasobów AzureResourceMonthlyUsageRecord, aby uzyskać listę usług w ramach subskrypcji klienta i skojarzonych z nimi informacji o użyciu.
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: khpavan
ms.author: sakhanda
ms.openlocfilehash: ee4bd413eec7d5a2dddbe3803df8839589ab7504
ms.sourcegitcommit: d4b0c80d81f1d5bdf3c4c03344ad639646ae6ab9
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/09/2021
ms.locfileid: "111760287"
---
# <a name="get-all-monthly-usage-records-for-a-subscription"></a><span data-ttu-id="13f06-103">Pobieranie wszystkich rekordów dotyczących miesięcznego użycia dla subskrypcji</span><span class="sxs-lookup"><span data-stu-id="13f06-103">Get all monthly usage records for a subscription</span></span>

<span data-ttu-id="13f06-104">**Dotyczy:** Partner Center | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="13f06-104">**Applies to**: Partner Center | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="13f06-105">Możesz użyć kolekcji zasobów [**AzureResourceMonthlyUsageRecord,**](/dotnet/api/microsoft.store.partnercenter.models.usage.azureresourcemonthlyusagerecord) aby uzyskać listę usług w ramach subskrypcji klienta i skojarzonych z nimi informacji o użyciu.</span><span class="sxs-lookup"><span data-stu-id="13f06-105">You can use the [**AzureResourceMonthlyUsageRecord**](/dotnet/api/microsoft.store.partnercenter.models.usage.azureresourcemonthlyusagerecord) resource collection to get a list of services within a customer's subscription and their associated rated usage information.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="13f06-106">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="13f06-106">Prerequisites</span></span>

- <span data-ttu-id="13f06-107">Poświadczenia zgodnie z opisem w [te Partner Center uwierzytelniania.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="13f06-107">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="13f06-108">Ten scenariusz obsługuje uwierzytelnianie przy użyciu zarówno poświadczeń aplikacji autonomicznej, jak i aplikacji i użytkownika.</span><span class="sxs-lookup"><span data-stu-id="13f06-108">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="13f06-109">Identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="13f06-109">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="13f06-110">Jeśli nie znasz identyfikatora klienta, możesz go znaleźć na pulpicie nawigacyjnym Partner Center [nawigacyjnym](https://partner.microsoft.com/dashboard).</span><span class="sxs-lookup"><span data-stu-id="13f06-110">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="13f06-111">Wybierz **pozycję CSP** z menu Partner Center, a następnie pozycję **Klienci.**</span><span class="sxs-lookup"><span data-stu-id="13f06-111">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="13f06-112">Wybierz klienta z listy klientów, a następnie wybierz **pozycję Konto**.</span><span class="sxs-lookup"><span data-stu-id="13f06-112">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="13f06-113">Na stronie Konto klienta poszukaj identyfikatora **Microsoft w** sekcji Informacje o **koncie** klienta.</span><span class="sxs-lookup"><span data-stu-id="13f06-113">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="13f06-114">Identyfikator microsoft jest taki sam jak identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="13f06-114">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="13f06-115">Identyfikator subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="13f06-115">A subscription identifier.</span></span>

<span data-ttu-id="13f06-116">*Ten interfejs API obsługuje Microsoft Azure subskrypcji (MS-AZR-0145P). Jeśli używasz planu platformy Azure, zobacz Zamiast tego zobacz [Get usage data for subscription by meter (Uzyskiwanie](get-a-customer-subscription-meter-usage-records.md) danych użycia dla subskrypcji według miernika).*</span><span class="sxs-lookup"><span data-stu-id="13f06-116">*This API only supports Microsoft Azure (MS-AZR-0145P) subscriptions. If you are using an Azure plan, see [Get usage data for subscription by meter](get-a-customer-subscription-meter-usage-records.md) instead.*</span></span>

## <a name="c"></a><span data-ttu-id="13f06-117">C\#</span><span class="sxs-lookup"><span data-stu-id="13f06-117">C\#</span></span>

<span data-ttu-id="13f06-118">Aby uzyskać informacje o użyciu zasobów subskrypcji:</span><span class="sxs-lookup"><span data-stu-id="13f06-118">To get a subscription's resource usage information:</span></span>

1. <span data-ttu-id="13f06-119">Użyj **kolekcji IAggregatePartner.Customers,** aby wywołać **metodę ById().**</span><span class="sxs-lookup"><span data-stu-id="13f06-119">Use your **IAggregatePartner.Customers** collection to call the **ById()** method.</span></span>

2. <span data-ttu-id="13f06-120">Wywołaj **właściwości Subscriptions** i **UsageRecords,** a następnie **właściwość Resources.**</span><span class="sxs-lookup"><span data-stu-id="13f06-120">Call the **Subscriptions** property, and **UsageRecords**, then the **Resources** property.</span></span>
3. <span data-ttu-id="13f06-121">Wywołaj **metody Get()** **lub GetAsync().**</span><span class="sxs-lookup"><span data-stu-id="13f06-121">Call the **Get()** or **GetAsync()** methods.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// var selectedCustomerId as string;
// var selectedSubscriptionID as string;

var usageRecords = partnerOperations.Customers.ById(selectedCustomerId).Subscriptions.ById(selectedSubscriptionId).UsageRecords.Resources.Get();
```

<span data-ttu-id="13f06-122">Przykład można znaleźć w następujących tematach:</span><span class="sxs-lookup"><span data-stu-id="13f06-122">For an example, see the following:</span></span>

- <span data-ttu-id="13f06-123">Przykład: [aplikacja testowa konsoli](console-test-app.md)</span><span class="sxs-lookup"><span data-stu-id="13f06-123">Sample: [Console test app](console-test-app.md)</span></span>
- <span data-ttu-id="13f06-124">Project: **PartnerSDK.FeatureSample**</span><span class="sxs-lookup"><span data-stu-id="13f06-124">Project: **PartnerSDK.FeatureSample**</span></span>
- <span data-ttu-id="13f06-125">Klasa: **SubscriptionResourceUsageRecords.cs**</span><span class="sxs-lookup"><span data-stu-id="13f06-125">Class: **SubscriptionResourceUsageRecords.cs**</span></span>

## <a name="rest-request"></a><span data-ttu-id="13f06-126">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="13f06-126">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="13f06-127">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="13f06-127">Request syntax</span></span>

| <span data-ttu-id="13f06-128">Metoda</span><span class="sxs-lookup"><span data-stu-id="13f06-128">Method</span></span>  | <span data-ttu-id="13f06-129">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="13f06-129">Request URI</span></span>                                                                                                                                       |
|---------|---------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="13f06-130">**Pobierz**</span><span class="sxs-lookup"><span data-stu-id="13f06-130">**GET**</span></span> | <span data-ttu-id="13f06-131">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/subscriptions/{id-for-subscription}/usagerecords/resources HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="13f06-131">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/subscriptions/{id-for-subscription}/usagerecords/resources HTTP/1.1</span></span> |

#### <a name="uri-parameters"></a><span data-ttu-id="13f06-132">Parametry URI</span><span class="sxs-lookup"><span data-stu-id="13f06-132">URI parameters</span></span>

<span data-ttu-id="13f06-133">W tej tabeli wymieniono wymagane parametry zapytania w celu uzyskania informacji o użyciu.</span><span class="sxs-lookup"><span data-stu-id="13f06-133">This table lists the required query parameters to get the rated usage information.</span></span>

| <span data-ttu-id="13f06-134">Nazwa</span><span class="sxs-lookup"><span data-stu-id="13f06-134">Name</span></span>                    | <span data-ttu-id="13f06-135">Typ</span><span class="sxs-lookup"><span data-stu-id="13f06-135">Type</span></span>     | <span data-ttu-id="13f06-136">Wymagane</span><span class="sxs-lookup"><span data-stu-id="13f06-136">Required</span></span> | <span data-ttu-id="13f06-137">Opis</span><span class="sxs-lookup"><span data-stu-id="13f06-137">Description</span></span>                               |
|-------------------------|----------|----------|-------------------------------------------|
| <span data-ttu-id="13f06-138">**identyfikator dzierżawy klienta**</span><span class="sxs-lookup"><span data-stu-id="13f06-138">**customer-tenant-id**</span></span>  | <span data-ttu-id="13f06-139">**guid**</span><span class="sxs-lookup"><span data-stu-id="13f06-139">**guid**</span></span> | <span data-ttu-id="13f06-140">Y</span><span class="sxs-lookup"><span data-stu-id="13f06-140">Y</span></span>        | <span data-ttu-id="13f06-141">Identyfikator GUID odpowiadający klientowi.</span><span class="sxs-lookup"><span data-stu-id="13f06-141">A GUID corresponding to the customer.</span></span>     |
| <span data-ttu-id="13f06-142">**subscription-id**</span><span class="sxs-lookup"><span data-stu-id="13f06-142">**subscription-id**</span></span> | <span data-ttu-id="13f06-143">**guid**</span><span class="sxs-lookup"><span data-stu-id="13f06-143">**guid**</span></span> | <span data-ttu-id="13f06-144">Y</span><span class="sxs-lookup"><span data-stu-id="13f06-144">Y</span></span>        | <span data-ttu-id="13f06-145">Identyfikator GUID odpowiadający subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="13f06-145">A GUID corresponding to the subscription.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="13f06-146">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="13f06-146">Request headers</span></span>

<span data-ttu-id="13f06-147">Aby uzyskać więcej informacji, [zobacz Partner Center REST headers (Nagłówki REST).](headers.md)</span><span class="sxs-lookup"><span data-stu-id="13f06-147">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="13f06-148">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="13f06-148">Request body</span></span>

<span data-ttu-id="13f06-149">Brak.</span><span class="sxs-lookup"><span data-stu-id="13f06-149">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="13f06-150">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="13f06-150">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/{customer-tenant-id}/subscriptions/{id-for-subscription}/usagerecords/resources HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 65b26053-37d0-4303-9fd1-46ad8012bcb6
MS-CorrelationId: 47c36033-af5d-4457-80a4-512c1626fac4
```

## <a name="rest-response"></a><span data-ttu-id="13f06-151">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="13f06-151">REST response</span></span>

<span data-ttu-id="13f06-152">W przypadku powodzenia ta metoda zwraca kolekcję zasobów **AzureResourceMonthlyUsageRecord** w treści odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="13f06-152">If successful, this method returns a collection of **AzureResourceMonthlyUsageRecord** resources in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="13f06-153">Kody powodzenia i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="13f06-153">Response success and error codes</span></span>

<span data-ttu-id="13f06-154">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie, oraz dodatkowe informacje o debugowaniu.</span><span class="sxs-lookup"><span data-stu-id="13f06-154">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="13f06-155">Użyj narzędzia śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="13f06-155">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="13f06-156">Aby uzyskać pełną listę, zobacz [Kody błędów](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="13f06-156">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="13f06-157">Przykład odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="13f06-157">Response example</span></span>

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
