---
title: Pobieranie wszystkich rekordów dotyczących użycia subskrypcji dla klienta
description: Kolekcji zasobów SubscriptionMonthlyUsageRecord można użyć do pobierania rekordów użycia subskrypcji dla klienta określonej usługi lub zasobu platformy Azure w bieżącym okresie rozliczeniowym.
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 976abd86f34c1c27184f277ffc89fbc65f16bb37
ms.sourcegitcommit: b1d6fd0ca93d8a3e30e970844d3164454415f553
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/09/2021
ms.locfileid: "111874690"
---
# <a name="get-subscription-usage-records-for-a-customer"></a><span data-ttu-id="0075b-103">Uzyskiwanie rekordów użycia subskrypcji dla klienta</span><span class="sxs-lookup"><span data-stu-id="0075b-103">Get subscription usage records for a customer</span></span>

<span data-ttu-id="0075b-104">**Dotyczy:** Partner Center | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="0075b-104">**Applies to**: Partner Center | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="0075b-105">Kolekcji zasobów **SubscriptionMonthlyUsageRecord** można użyć do pobierania rekordów użycia subskrypcji dla klienta określonej usługi lub zasobu platformy Azure w bieżącym okresie rozliczeniowym.</span><span class="sxs-lookup"><span data-stu-id="0075b-105">You can use the **SubscriptionMonthlyUsageRecord** resource collection to get subscription usage records for a customer of a specific Azure service or resource during the current billing period.</span></span> <span data-ttu-id="0075b-106">Ten zasób reprezentuje wszystkie subskrypcje dla klienta.</span><span class="sxs-lookup"><span data-stu-id="0075b-106">This resource represents all subscriptions for the customer.</span></span> <span data-ttu-id="0075b-107">W przypadku klienta z planem platformy Azure ten zasób zwraca listę tych planów (nie pojedynczych subskrypcji platformy Azure).</span><span class="sxs-lookup"><span data-stu-id="0075b-107">For a customer with an Azure plan, this resource returns a list of those plans (not individual Azure subscriptions).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0075b-108">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="0075b-108">Prerequisites</span></span>

- <span data-ttu-id="0075b-109">Poświadczenia zgodnie z opisem w te [Partner Center uwierzytelniania.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="0075b-109">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="0075b-110">Ten scenariusz obsługuje uwierzytelnianie tylko przy użyciu poświadczeń aplikacji i użytkownika.</span><span class="sxs-lookup"><span data-stu-id="0075b-110">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="0075b-111">Identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="0075b-111">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="0075b-112">Jeśli nie znasz identyfikatora klienta, możesz go znaleźć na pulpicie nawigacyjnym Partner Center [nawigacyjnym](https://partner.microsoft.com/dashboard).</span><span class="sxs-lookup"><span data-stu-id="0075b-112">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="0075b-113">Wybierz **pozycję CSP** z Partner Center menu, a następnie pozycję **Klienci.**</span><span class="sxs-lookup"><span data-stu-id="0075b-113">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="0075b-114">Wybierz klienta z listy klientów, a następnie wybierz pozycję **Konto**.</span><span class="sxs-lookup"><span data-stu-id="0075b-114">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="0075b-115">Na stronie Konto klienta odszukaj identyfikator **Microsoft w** **sekcji Informacje o koncie** klienta.</span><span class="sxs-lookup"><span data-stu-id="0075b-115">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="0075b-116">Identyfikator microsoft jest taki sam jak identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="0075b-116">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="c"></a><span data-ttu-id="0075b-117">C\#</span><span class="sxs-lookup"><span data-stu-id="0075b-117">C\#</span></span>

<span data-ttu-id="0075b-118">Aby uzyskać rekordy użycia subskrypcji dla klienta określonej usługi lub zasobu platformy Azure w bieżącym okresie rozliczeniowym, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="0075b-118">To get subscription usage records for a customer of a specific Azure service or resource during the current billing period, do the following steps:</span></span>

1. <span data-ttu-id="0075b-119">Użyj **kolekcji IAggregatePartner.Customers,** aby wywołać **metodę ById().**</span><span class="sxs-lookup"><span data-stu-id="0075b-119">Use your **IAggregatePartner.Customers** collection to call the **ById()** method.</span></span>

2. <span data-ttu-id="0075b-120">Następnie **wywołaj właściwość Subscriptions** i **właściwość UsageRecords.**</span><span class="sxs-lookup"><span data-stu-id="0075b-120">Then call the **Subscriptions** property and the **UsageRecords** property.</span></span> <span data-ttu-id="0075b-121">Zakończ, wywołując metody Get() lub GetAsync().</span><span class="sxs-lookup"><span data-stu-id="0075b-121">Finish by calling the Get() or GetAsync() methods.</span></span>

    ``` csharp
    // IAggregatePartner partnerOperations;
    // var selectedCustomerId as string;

    var usageRecords = partnerOperations.Customers.ById(selectedCustomerId).Subscriptions.UsageRecords.Get();
    ```

<span data-ttu-id="0075b-122">Przykład można znaleźć w następujących tematach:</span><span class="sxs-lookup"><span data-stu-id="0075b-122">For an example, see the following:</span></span>

- <span data-ttu-id="0075b-123">Przykład: [aplikacja testowa konsoli](console-test-app.md)</span><span class="sxs-lookup"><span data-stu-id="0075b-123">Sample: [Console test app](console-test-app.md)</span></span>
- <span data-ttu-id="0075b-124">Project: **PartnerSDK.FeatureSamples**</span><span class="sxs-lookup"><span data-stu-id="0075b-124">Project: **PartnerSDK.FeatureSamples**</span></span>
- <span data-ttu-id="0075b-125">Klasa: **GetSubscriptionUsageRecords.cs**</span><span class="sxs-lookup"><span data-stu-id="0075b-125">Class: **GetSubscriptionUsageRecords.cs**</span></span>

## <a name="rest-request"></a><span data-ttu-id="0075b-126">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="0075b-126">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="0075b-127">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="0075b-127">Request syntax</span></span>

| <span data-ttu-id="0075b-128">Metoda</span><span class="sxs-lookup"><span data-stu-id="0075b-128">Method</span></span>  | <span data-ttu-id="0075b-129">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="0075b-129">Request URI</span></span>                                                                                                      |
|---------|------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="0075b-130">**Pobierz**</span><span class="sxs-lookup"><span data-stu-id="0075b-130">**GET**</span></span> | <span data-ttu-id="0075b-131">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{identyfikator-dzierżawy-klienta}/subscriptions/usagerecords HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="0075b-131">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/subscriptions/usagerecords HTTP/1.1</span></span> |

#### <a name="uri-parameter"></a><span data-ttu-id="0075b-132">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="0075b-132">URI parameter</span></span>

<span data-ttu-id="0075b-133">W tej tabeli wymieniono wymagany parametr zapytania w celu uzyskania informacji o użyciu ocenionym przez klienta.</span><span class="sxs-lookup"><span data-stu-id="0075b-133">This table lists the required query parameter to get the customer's rated usage information.</span></span>

| <span data-ttu-id="0075b-134">Nazwa</span><span class="sxs-lookup"><span data-stu-id="0075b-134">Name</span></span>                   | <span data-ttu-id="0075b-135">Typ</span><span class="sxs-lookup"><span data-stu-id="0075b-135">Type</span></span>     | <span data-ttu-id="0075b-136">Wymagane</span><span class="sxs-lookup"><span data-stu-id="0075b-136">Required</span></span> | <span data-ttu-id="0075b-137">Opis</span><span class="sxs-lookup"><span data-stu-id="0075b-137">Description</span></span>                           |
|------------------------|----------|----------|---------------------------------------|
| <span data-ttu-id="0075b-138">**identyfikator dzierżawy klienta**</span><span class="sxs-lookup"><span data-stu-id="0075b-138">**customer-tenant-id**</span></span> | <span data-ttu-id="0075b-139">**guid**</span><span class="sxs-lookup"><span data-stu-id="0075b-139">**guid**</span></span> | <span data-ttu-id="0075b-140">Y</span><span class="sxs-lookup"><span data-stu-id="0075b-140">Y</span></span>        | <span data-ttu-id="0075b-141">Identyfikator GUID odpowiadający klientowi.</span><span class="sxs-lookup"><span data-stu-id="0075b-141">A GUID corresponding to the customer.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="0075b-142">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="0075b-142">Request headers</span></span>

<span data-ttu-id="0075b-143">Aby uzyskać więcej informacji, [zobacz Partner Center REST headers (Nagłówki REST).](headers.md)</span><span class="sxs-lookup"><span data-stu-id="0075b-143">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="0075b-144">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="0075b-144">Request body</span></span>

<span data-ttu-id="0075b-145">Brak.</span><span class="sxs-lookup"><span data-stu-id="0075b-145">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="0075b-146">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="0075b-146">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/{customer-tenant-id}/subscriptions/usagerecords HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: e128c8e2-4c33-4940-a3e2-2e59b0abdc67
MS-CorrelationId: 47c36033-af5d-4457-80a4-512c1626fac4
```

## <a name="rest-response"></a><span data-ttu-id="0075b-147">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="0075b-147">REST response</span></span>

<span data-ttu-id="0075b-148">W przypadku powodzenia ta metoda zwraca **zasób SubscriptionMonthlyUsageRecord** w treści odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="0075b-148">If successful, this method returns a **SubscriptionMonthlyUsageRecord** resource in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="0075b-149">Kody powodzenia i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="0075b-149">Response success and error codes</span></span>

<span data-ttu-id="0075b-150">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie, oraz dodatkowe informacje o debugowaniu.</span><span class="sxs-lookup"><span data-stu-id="0075b-150">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="0075b-151">Użyj narzędzia śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="0075b-151">Use a network trace tool to read this code, the error type, and additional parameters.</span></span> <span data-ttu-id="0075b-152">Aby uzyskać pełną listę, zobacz [Kody błędów](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="0075b-152">For a full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example-for-microsoft-azure-ms-azr-0145p-subscriptions"></a><span data-ttu-id="0075b-153">Przykład odpowiedzi dla Microsoft Azure subskrypcji (MS-AZR-0145P)</span><span class="sxs-lookup"><span data-stu-id="0075b-153">Response example for Microsoft Azure (MS-AZR-0145P) subscriptions</span></span>

<span data-ttu-id="0075b-154">W tym przykładzie klient kupił ofertę **Azure PayG 145P.**</span><span class="sxs-lookup"><span data-stu-id="0075b-154">In this example, the customer purchased a **145P Azure PayG** offer.</span></span>

<span data-ttu-id="0075b-155">*W przypadku klientów Microsoft Azure subskrypcji interfejsu API (MS-AZR-0145P) nie ma żadnych zmian w odpowiedzi interfejsu API.*</span><span class="sxs-lookup"><span data-stu-id="0075b-155">*For customers with Microsoft Azure (MS-AZR-0145P) subscriptions, there will be no change to the API response.*</span></span>

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
            "uri": "/customers/<customer-tenant-id>/subscriptions/usagerecords/",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "Collection"
    }
}
```

## <a name="rest-response-example-for-azure-plan"></a><span data-ttu-id="0075b-156">Przykład odpowiedzi REST dla planu platformy Azure</span><span class="sxs-lookup"><span data-stu-id="0075b-156">REST response example for Azure plan</span></span>

<span data-ttu-id="0075b-157">W tym przykładzie klient kupił plan platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="0075b-157">In this example, the customer purchased an Azure plan.</span></span>

<span data-ttu-id="0075b-158">*W przypadku klientów korzystających z planów platformy Azure w odpowiedzi interfejsu API występują następujące zmiany:*</span><span class="sxs-lookup"><span data-stu-id="0075b-158">*For customers with Azure plans, there are the following changes in the API response:*</span></span>

- <span data-ttu-id="0075b-159">**CurrencyLocale został** zastąpiony wartością **currencyCode**</span><span class="sxs-lookup"><span data-stu-id="0075b-159">**currencyLocale** is replaced with **currencyCode**</span></span>
- <span data-ttu-id="0075b-160">**USDTotalCost** to nowe pole</span><span class="sxs-lookup"><span data-stu-id="0075b-160">**usdTotalCost** is a new field</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 1120
Content-Type: application/json
MS-CorrelationId: 47c36033-af5d-4457-80a4-512c1626fac4
MS-RequestId: e128c8e2-4c33-4940-a3e2-2e59b0abdc67
Date: Tue, 17 Sep 2019 20:31:45 GMT

{
    "totalCount": 2,
    "items": [
        {
            "status": "active",
            "partnerOnRecord": "some-id",
            "offerId": "DZH318Z0BPS6:0001:DZH318Z0BML6",
            "resourceId": "11111111-7d58-6654-69fa-0797198155d3",
            "id": "11111111-7d58-6654-69fa-0797198155d3",
            "resourceName": "Azure plan",
            "name": "Azure plan",
            "totalCost": 0,
            "currencyCode": "GBP",
            "usdTotalCost": 0,
            "lastModifiedDate": "2019-09-18T17:09:26.16+00:00",
            "attributes": {
                "objectType": "SubscriptionMonthlyUsageRecord"
            }
        },
        {
            "status": "active",
            "partnerOnRecord": "some-id",
            "offerId": "DZH318Z0BPS6:0001:DZH318Z0BML6",
            "resourceId": "11111111-25aa-ebb8-2bb4-fb406307babd",
            "id": "11111111-25aa-ebb8-2bb4-fb406307babd",
            "resourceName": "Azure plan",
            "name": "Azure plan",
            "totalCost": 0,
            "currencyCode": "GBP",
            "usdTotalCost": 0,
            "lastModifiedDate": "2019-09-18T17:09:26.16+00:00",
            "attributes": {
                "objectType": "SubscriptionMonthlyUsageRecord"
            }
        }
    ],
    "links": {
        "self": {
            "uri": "/customers/<customer-tenant-id>/subscriptions/usagerecords",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "Collection"
    }
}
```
