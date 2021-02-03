---
title: Pobieranie wszystkich rekordów dotyczących użycia subskrypcji dla klienta
description: Kolekcji zasobów SubscriptionMonthlyUsageRecord można użyć do uzyskania rekordów użycia subskrypcji dla klienta określonej usługi lub zasobu platformy Azure w bieżącym okresie rozliczeniowym.
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 765ea16ff58b462d83ae3b8764b8b34c3ef804dc
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/08/2020
ms.locfileid: "97767970"
---
# <a name="get-subscription-usage-records-for-a-customer"></a><span data-ttu-id="b19b9-103">Pobieranie rekordów użycia subskrypcji dla klienta</span><span class="sxs-lookup"><span data-stu-id="b19b9-103">Get subscription usage records for a customer</span></span>

<span data-ttu-id="b19b9-104">**Dotyczy:**</span><span class="sxs-lookup"><span data-stu-id="b19b9-104">**Applies to:**</span></span>

- <span data-ttu-id="b19b9-105">Centrum partnerskie</span><span class="sxs-lookup"><span data-stu-id="b19b9-105">Partner Center</span></span>
- <span data-ttu-id="b19b9-106">Centrum partnerskie dla Microsoft Cloud Niemcy</span><span class="sxs-lookup"><span data-stu-id="b19b9-106">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="b19b9-107">Centrum partnerskie Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="b19b9-107">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="b19b9-108">Kolekcji zasobów **SubscriptionMonthlyUsageRecord** można użyć do uzyskania rekordów użycia subskrypcji dla klienta określonej usługi lub zasobu platformy Azure w bieżącym okresie rozliczeniowym.</span><span class="sxs-lookup"><span data-stu-id="b19b9-108">You can use the **SubscriptionMonthlyUsageRecord** resource collection to get subscription usage records for a customer of a specific Azure service or resource during the current billing period.</span></span> <span data-ttu-id="b19b9-109">Ten zasób reprezentuje wszystkie subskrypcje dla klienta.</span><span class="sxs-lookup"><span data-stu-id="b19b9-109">This resource represents all subscriptions for the customer.</span></span> <span data-ttu-id="b19b9-110">W przypadku klienta z planem platformy Azure ten zasób zwraca listę tych planów (nie poszczególnych subskrypcji platformy Azure).</span><span class="sxs-lookup"><span data-stu-id="b19b9-110">For a customer with an Azure plan, this resource returns a list of those plans (not individual Azure subscriptions).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b19b9-111">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="b19b9-111">Prerequisites</span></span>

- <span data-ttu-id="b19b9-112">Poświadczenia zgodnie z opisem w temacie [uwierzytelnianie w centrum partnerskim](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="b19b9-112">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="b19b9-113">Ten scenariusz obsługuje tylko uwierzytelnianie przy użyciu aplikacji i poświadczeń użytkownika.</span><span class="sxs-lookup"><span data-stu-id="b19b9-113">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="b19b9-114">Identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="b19b9-114">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="b19b9-115">Jeśli nie znasz identyfikatora klienta, możesz go wyszukać na [pulpicie nawigacyjnym](https://partner.microsoft.com/dashboard)Centrum partnerskiego.</span><span class="sxs-lookup"><span data-stu-id="b19b9-115">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="b19b9-116">Wybierz pozycję **dostawca CSP** z menu Centrum partnerskiego, po którym znajdują się **klienci**.</span><span class="sxs-lookup"><span data-stu-id="b19b9-116">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="b19b9-117">Wybierz klienta z listy klient, a następnie wybierz pozycję **konto**.</span><span class="sxs-lookup"><span data-stu-id="b19b9-117">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="b19b9-118">Na stronie konto klienta Znajdź **Identyfikator Microsoft** w sekcji **Informacje o koncie klienta** .</span><span class="sxs-lookup"><span data-stu-id="b19b9-118">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="b19b9-119">Identyfikator Microsoft jest taki sam jak identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="b19b9-119">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="c"></a><span data-ttu-id="b19b9-120">C\#</span><span class="sxs-lookup"><span data-stu-id="b19b9-120">C\#</span></span>

<span data-ttu-id="b19b9-121">Pobieranie rekordów użycia subskrypcji dla klienta określonej usługi lub zasobu platformy Azure w bieżącym okresie rozliczeniowym.:</span><span class="sxs-lookup"><span data-stu-id="b19b9-121">To get subscription usage records for a customer of a specific Azure service or resource during the current billing period.:</span></span>

1. <span data-ttu-id="b19b9-122">Użyj kolekcji **IAggregatePartner. Customers** , aby wywołać metodę **ById ()** .</span><span class="sxs-lookup"><span data-stu-id="b19b9-122">Use your **IAggregatePartner.Customers** collection to call the **ById()** method.</span></span>

2. <span data-ttu-id="b19b9-123">Następnie Wywołaj Właściwość **subscriptions** , a także właściwość **UsageRecords** .</span><span class="sxs-lookup"><span data-stu-id="b19b9-123">Then call the **Subscriptions** property, as well as **UsageRecords** property.</span></span> <span data-ttu-id="b19b9-124">Zakończ, wywołując metody get () lub GetAsync ().</span><span class="sxs-lookup"><span data-stu-id="b19b9-124">Finish by calling the Get() or GetAsync() methods.</span></span>

    ``` csharp
    // IAggregatePartner partnerOperations;
    // var selectedCustomerId as string;

    var usageRecords = partnerOperations.Customers.ById(selectedCustomerId).Subscriptions.UsageRecords.Get();
    ```

<span data-ttu-id="b19b9-125">Aby zapoznać się z przykładem, zobacz następujące tematy:</span><span class="sxs-lookup"><span data-stu-id="b19b9-125">For an example, see the following:</span></span>

- <span data-ttu-id="b19b9-126">Przykład: [aplikacja testowa konsoli](console-test-app.md)</span><span class="sxs-lookup"><span data-stu-id="b19b9-126">Sample: [Console test app](console-test-app.md)</span></span>
- <span data-ttu-id="b19b9-127">Projekt: **PartnerSDK. FeatureSamples**</span><span class="sxs-lookup"><span data-stu-id="b19b9-127">Project: **PartnerSDK.FeatureSamples**</span></span>
- <span data-ttu-id="b19b9-128">Klasa: **GetSubscriptionUsageRecords.cs**</span><span class="sxs-lookup"><span data-stu-id="b19b9-128">Class: **GetSubscriptionUsageRecords.cs**</span></span>

## <a name="rest-request"></a><span data-ttu-id="b19b9-129">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="b19b9-129">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="b19b9-130">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="b19b9-130">Request syntax</span></span>

| <span data-ttu-id="b19b9-131">Metoda</span><span class="sxs-lookup"><span data-stu-id="b19b9-131">Method</span></span>  | <span data-ttu-id="b19b9-132">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="b19b9-132">Request URI</span></span>                                                                                                      |
|---------|------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="b19b9-133">**Pobierz**</span><span class="sxs-lookup"><span data-stu-id="b19b9-133">**GET**</span></span> | <span data-ttu-id="b19b9-134">[*{baseURL}*](partner-center-rest-urls.md)/V1/Customers/{Customer-tenant-ID}/subscriptions/usagerecords http/1.1</span><span class="sxs-lookup"><span data-stu-id="b19b9-134">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/subscriptions/usagerecords HTTP/1.1</span></span> |

#### <a name="uri-parameter"></a><span data-ttu-id="b19b9-135">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="b19b9-135">URI parameter</span></span>

<span data-ttu-id="b19b9-136">W tej tabeli przedstawiono parametr zapytania wymaganego do uzyskania informacji o znamionowym użyciu klienta.</span><span class="sxs-lookup"><span data-stu-id="b19b9-136">This table lists the required query parameter to get the customer's rated usage information.</span></span>

| <span data-ttu-id="b19b9-137">Nazwa</span><span class="sxs-lookup"><span data-stu-id="b19b9-137">Name</span></span>                   | <span data-ttu-id="b19b9-138">Typ</span><span class="sxs-lookup"><span data-stu-id="b19b9-138">Type</span></span>     | <span data-ttu-id="b19b9-139">Wymagane</span><span class="sxs-lookup"><span data-stu-id="b19b9-139">Required</span></span> | <span data-ttu-id="b19b9-140">Opis</span><span class="sxs-lookup"><span data-stu-id="b19b9-140">Description</span></span>                           |
|------------------------|----------|----------|---------------------------------------|
| <span data-ttu-id="b19b9-141">**Identyfikator dzierżawy klienta**</span><span class="sxs-lookup"><span data-stu-id="b19b9-141">**customer-tenant-id**</span></span> | <span data-ttu-id="b19b9-142">**guid**</span><span class="sxs-lookup"><span data-stu-id="b19b9-142">**guid**</span></span> | <span data-ttu-id="b19b9-143">Y</span><span class="sxs-lookup"><span data-stu-id="b19b9-143">Y</span></span>        | <span data-ttu-id="b19b9-144">Identyfikator GUID odpowiadający klientowi.</span><span class="sxs-lookup"><span data-stu-id="b19b9-144">A GUID corresponding to the customer.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="b19b9-145">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="b19b9-145">Request headers</span></span>

<span data-ttu-id="b19b9-146">Aby uzyskać więcej informacji, zobacz [nagłówki REST Centrum partnerskiego](headers.md).</span><span class="sxs-lookup"><span data-stu-id="b19b9-146">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="b19b9-147">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="b19b9-147">Request body</span></span>

<span data-ttu-id="b19b9-148">Brak.</span><span class="sxs-lookup"><span data-stu-id="b19b9-148">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="b19b9-149">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="b19b9-149">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/{customer-tenant-id}/subscriptions/usagerecords HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: e128c8e2-4c33-4940-a3e2-2e59b0abdc67
MS-CorrelationId: 47c36033-af5d-4457-80a4-512c1626fac4
```

## <a name="rest-response"></a><span data-ttu-id="b19b9-150">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="b19b9-150">REST response</span></span>

<span data-ttu-id="b19b9-151">Jeśli to się powiedzie, metoda zwraca zasób **SubscriptionMonthlyUsageRecord** w treści odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="b19b9-151">If successful, this method returns a **SubscriptionMonthlyUsageRecord** resource in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="b19b9-152">Kody sukcesu i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="b19b9-152">Response success and error codes</span></span>

<span data-ttu-id="b19b9-153">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie i dodatkowe informacje debugowania.</span><span class="sxs-lookup"><span data-stu-id="b19b9-153">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="b19b9-154">Użyj narzędzia do śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="b19b9-154">Use a network trace tool to read this code, the error type, and additional parameters.</span></span> <span data-ttu-id="b19b9-155">Aby uzyskać pełną listę, zobacz [kody błędów](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="b19b9-155">For a full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example-for-microsoft-azure-ms-azr-0145p-subscriptions"></a><span data-ttu-id="b19b9-156">Przykład odpowiedzi dla subskrypcji Microsoft Azure (MS-AZR-0145P)</span><span class="sxs-lookup"><span data-stu-id="b19b9-156">Response example for Microsoft Azure (MS-AZR-0145P) subscriptions</span></span>

<span data-ttu-id="b19b9-157">W tym przykładzie klient zakupił ofertę **145Pą platformy Azure** .</span><span class="sxs-lookup"><span data-stu-id="b19b9-157">In this example, the customer purchased a **145P Azure PayG** offer.</span></span>

<span data-ttu-id="b19b9-158">*W przypadku klientów z subskrypcjami Microsoft Azure (MS-AZR-0145P) nie będzie zmieniana odpowiedź interfejsu API.*</span><span class="sxs-lookup"><span data-stu-id="b19b9-158">*For customers with Microsoft Azure (MS-AZR-0145P) subscriptions, there will be no change to the API response.*</span></span>

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

## <a name="rest-response-example-for-azure-plan"></a><span data-ttu-id="b19b9-159">Przykład odpowiedzi REST dla usługi Azure plan</span><span class="sxs-lookup"><span data-stu-id="b19b9-159">REST response example for Azure plan</span></span>

<span data-ttu-id="b19b9-160">W tym przykładzie klient kupił plan platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="b19b9-160">In this example, the customer purchased an Azure plan.</span></span>

<span data-ttu-id="b19b9-161">*W przypadku klientów z planami platformy Azure w odpowiedzi interfejsu API istnieją następujące zmiany:*</span><span class="sxs-lookup"><span data-stu-id="b19b9-161">*For customers with Azure plans, there are the following changes in the API response:*</span></span>

- <span data-ttu-id="b19b9-162">**currencyLocale** został zastąpiony **CurrencyCode**</span><span class="sxs-lookup"><span data-stu-id="b19b9-162">**currencyLocale** is replaced with **currencyCode**</span></span>
- <span data-ttu-id="b19b9-163">**usdTotalCost** jest nowym polem</span><span class="sxs-lookup"><span data-stu-id="b19b9-163">**usdTotalCost** is a new field</span></span>

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
