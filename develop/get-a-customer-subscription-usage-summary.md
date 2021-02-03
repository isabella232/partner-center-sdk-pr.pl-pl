---
title: Pobierz Podsumowanie użycia dla subskrypcji klienta
description: Zasobu SubscriptionUsageSummary można użyć do uzyskania podsumowania użycia subskrypcji określonej usługi lub zasobu platformy Azure w bieżącym okresie rozliczeniowym.
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 30334b6f08829eccf0693b566c11f94cb3ece976
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/08/2020
ms.locfileid: "97767966"
---
# <a name="get-usage-summary-for-customers-subscription"></a><span data-ttu-id="2a655-103">Pobierz Podsumowanie użycia dla subskrypcji klienta</span><span class="sxs-lookup"><span data-stu-id="2a655-103">Get usage summary for customer's subscription</span></span>

<span data-ttu-id="2a655-104">**Dotyczy:**</span><span class="sxs-lookup"><span data-stu-id="2a655-104">**Applies to:**</span></span>

- <span data-ttu-id="2a655-105">Centrum partnerskie</span><span class="sxs-lookup"><span data-stu-id="2a655-105">Partner Center</span></span>
- <span data-ttu-id="2a655-106">Centrum partnerskie dla Microsoft Cloud Niemcy</span><span class="sxs-lookup"><span data-stu-id="2a655-106">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="2a655-107">Centrum partnerskie Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="2a655-107">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="2a655-108">Za pomocą zasobu **SubscriptionUsageSummary** można uzyskać podsumowanie użycia subskrypcji dla klienta.</span><span class="sxs-lookup"><span data-stu-id="2a655-108">You can use the **SubscriptionUsageSummary** resource to get a subscription usage summary for a customer.</span></span> <span data-ttu-id="2a655-109">Ten zasób reprezentuje Podsumowanie użycia subskrypcji określonej usługi lub zasobu platformy Azure w bieżącym okresie rozliczeniowym.</span><span class="sxs-lookup"><span data-stu-id="2a655-109">This resource represents the subscription usage summary of a specific Azure service or resource during the current billing period.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2a655-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="2a655-110">Prerequisites</span></span>

- <span data-ttu-id="2a655-111">Poświadczenia zgodnie z opisem w temacie [uwierzytelnianie w centrum partnerskim](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="2a655-111">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="2a655-112">Ten scenariusz obsługuje tylko uwierzytelnianie przy użyciu aplikacji i poświadczeń użytkownika.</span><span class="sxs-lookup"><span data-stu-id="2a655-112">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="2a655-113">Identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="2a655-113">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="2a655-114">Jeśli nie znasz identyfikatora klienta, możesz go wyszukać na [pulpicie nawigacyjnym](https://partner.microsoft.com/dashboard)Centrum partnerskiego.</span><span class="sxs-lookup"><span data-stu-id="2a655-114">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="2a655-115">Wybierz pozycję **dostawca CSP** z menu Centrum partnerskiego, po którym znajdują się **klienci**.</span><span class="sxs-lookup"><span data-stu-id="2a655-115">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="2a655-116">Wybierz klienta z listy klient, a następnie wybierz pozycję **konto**.</span><span class="sxs-lookup"><span data-stu-id="2a655-116">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="2a655-117">Na stronie konto klienta Znajdź **Identyfikator Microsoft** w sekcji **Informacje o koncie klienta** .</span><span class="sxs-lookup"><span data-stu-id="2a655-117">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="2a655-118">Identyfikator Microsoft jest taki sam jak identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="2a655-118">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="2a655-119">Identyfikator subskrypcji</span><span class="sxs-lookup"><span data-stu-id="2a655-119">A subscription identifier</span></span>

## <a name="c"></a><span data-ttu-id="2a655-120">C\#</span><span class="sxs-lookup"><span data-stu-id="2a655-120">C\#</span></span>

<span data-ttu-id="2a655-121">Aby uzyskać podsumowanie użycia subskrypcji dla subskrypcji klienta:</span><span class="sxs-lookup"><span data-stu-id="2a655-121">To get a subscription usage summary for a customer's subscription:</span></span>

1. <span data-ttu-id="2a655-122">Użyj kolekcji **IAggregatePartner. Customers** , aby wywołać metodę **ById ()** .</span><span class="sxs-lookup"><span data-stu-id="2a655-122">Use your **IAggregatePartner.Customers** collection to call the **ById()** method.</span></span>

2. <span data-ttu-id="2a655-123">Następnie Wywołaj Właściwość subscriptions, a także właściwość **UsageSummary** .</span><span class="sxs-lookup"><span data-stu-id="2a655-123">Then call the Subscriptions property, as well as **UsageSummary** property.</span></span> <span data-ttu-id="2a655-124">Zakończ, wywołując metody get () lub GetAsync ().</span><span class="sxs-lookup"><span data-stu-id="2a655-124">Finish by calling the Get() or GetAsync() methods.</span></span>

    ``` csharp
    // IAggregatePartner partnerOperations;
    // var selectedCustomerId as string;
    // var selectedSubscriptionId as string;

    var subscriptionUsageSummary = partnerOperations.Customers.ById(selectedCustomerId).Subscriptions.ById(selectedSubscriptionId).UsageSummary.Get();
    ```

<span data-ttu-id="2a655-125">Aby zapoznać się z przykładem, zobacz następujące tematy:</span><span class="sxs-lookup"><span data-stu-id="2a655-125">For an example, see the following:</span></span>

- <span data-ttu-id="2a655-126">Przykład: [aplikacja testowa konsoli](console-test-app.md)</span><span class="sxs-lookup"><span data-stu-id="2a655-126">Sample: [Console test app](console-test-app.md)</span></span>
- <span data-ttu-id="2a655-127">Projekt: **PartnerSDK. FeatureSamples**</span><span class="sxs-lookup"><span data-stu-id="2a655-127">Project: **PartnerSDK.FeatureSamples**</span></span>
- <span data-ttu-id="2a655-128">Klasa: **GetSubscriptionUsageSummary.cs**</span><span class="sxs-lookup"><span data-stu-id="2a655-128">Class: **GetSubscriptionUsageSummary.cs**</span></span>

## <a name="rest-request"></a><span data-ttu-id="2a655-129">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="2a655-129">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="2a655-130">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="2a655-130">Request syntax</span></span>

| <span data-ttu-id="2a655-131">Metoda</span><span class="sxs-lookup"><span data-stu-id="2a655-131">Method</span></span>  | <span data-ttu-id="2a655-132">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="2a655-132">Request URI</span></span>                                                                                                                        |
|---------|------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="2a655-133">**Pobierz**</span><span class="sxs-lookup"><span data-stu-id="2a655-133">**GET**</span></span> | <span data-ttu-id="2a655-134">[*{baseURL}*](partner-center-rest-urls.md)/V1/Customers/{Customer-tenant-ID}/subscriptions/{Subscription-ID}/usagesummary http/1.1</span><span class="sxs-lookup"><span data-stu-id="2a655-134">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/subscriptions/{subscription-id}/usagesummary HTTP/1.1</span></span> |

#### <a name="uri-parameters"></a><span data-ttu-id="2a655-135">Parametry identyfikatora URI</span><span class="sxs-lookup"><span data-stu-id="2a655-135">URI parameters</span></span>

<span data-ttu-id="2a655-136">Ta tabela zawiera listę wymaganych parametrów zapytania w celu uzyskania informacji o znamionowym użyciu klienta.</span><span class="sxs-lookup"><span data-stu-id="2a655-136">This table lists the required query parameters to get the customer's rated usage information.</span></span>

| <span data-ttu-id="2a655-137">Nazwa</span><span class="sxs-lookup"><span data-stu-id="2a655-137">Name</span></span>                   | <span data-ttu-id="2a655-138">Typ</span><span class="sxs-lookup"><span data-stu-id="2a655-138">Type</span></span>     | <span data-ttu-id="2a655-139">Wymagane</span><span class="sxs-lookup"><span data-stu-id="2a655-139">Required</span></span> | <span data-ttu-id="2a655-140">Opis</span><span class="sxs-lookup"><span data-stu-id="2a655-140">Description</span></span>                               |
|------------------------|----------|----------|-------------------------------------------|
| <span data-ttu-id="2a655-141">**Identyfikator dzierżawy klienta**</span><span class="sxs-lookup"><span data-stu-id="2a655-141">**customer-tenant-id**</span></span> | <span data-ttu-id="2a655-142">**guid**</span><span class="sxs-lookup"><span data-stu-id="2a655-142">**guid**</span></span> | <span data-ttu-id="2a655-143">Y</span><span class="sxs-lookup"><span data-stu-id="2a655-143">Y</span></span>        | <span data-ttu-id="2a655-144">Identyfikator GUID odpowiadający klientowi.</span><span class="sxs-lookup"><span data-stu-id="2a655-144">A GUID corresponding to the customer.</span></span>     |
| <span data-ttu-id="2a655-145">**Identyfikator subskrypcji**</span><span class="sxs-lookup"><span data-stu-id="2a655-145">**subscription-id**</span></span>    | <span data-ttu-id="2a655-146">**guid**</span><span class="sxs-lookup"><span data-stu-id="2a655-146">**guid**</span></span> | <span data-ttu-id="2a655-147">Y</span><span class="sxs-lookup"><span data-stu-id="2a655-147">Y</span></span>        | <span data-ttu-id="2a655-148">Identyfikator GUID odpowiadający identyfikatorowi subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="2a655-148">A GUID corresponding to the identifier of a subscription.</span></span> <span data-ttu-id="2a655-149">W przypadku planu platformy Azure jest to identyfikator odpowiedniego [zasobu subskrypcji](subscription-resources.md#subscription)Centrum partnerskiego, który reprezentuje plan platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="2a655-149">For an Azure plan, this is the identifier of the corresponding Partner Center [subscription resource](subscription-resources.md#subscription), which represents the Azure plan.</span></span> <span data-ttu-id="2a655-150">*W przypadku zasobów subskrypcji planu platformy Azure Podaj **identyfikator planu** jako **Identyfikator subskrypcji** w tej trasie.*</span><span class="sxs-lookup"><span data-stu-id="2a655-150">*For Azure plan subscription resources, provide the **plan-id** as the **subscription-id** in this route.*</span></span> |

### <a name="request-headers"></a><span data-ttu-id="2a655-151">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="2a655-151">Request headers</span></span>

<span data-ttu-id="2a655-152">Aby uzyskać więcej informacji, zobacz [nagłówki REST Centrum partnerskiego](headers.md).</span><span class="sxs-lookup"><span data-stu-id="2a655-152">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="2a655-153">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="2a655-153">Request body</span></span>

<span data-ttu-id="2a655-154">Brak.</span><span class="sxs-lookup"><span data-stu-id="2a655-154">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="2a655-155">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="2a655-155">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/{customer-tenant-id}/subscriptions/{subscription-id}/usagesummary HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: e128c8e2-4c33-4940-a3e2-2e59b0abdc67
MS-CorrelationId: 47c36033-af5d-4457-80a4-512c1626fac4
```

## <a name="rest-response"></a><span data-ttu-id="2a655-156">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="2a655-156">REST response</span></span>

<span data-ttu-id="2a655-157">Jeśli to się powiedzie, metoda zwraca zasób **SubscriptionUsageSummary** w treści odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="2a655-157">If successful, this method returns a **SubscriptionUsageSummary** resource in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="2a655-158">Kody sukcesu i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="2a655-158">Response success and error codes</span></span>

<span data-ttu-id="2a655-159">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie i dodatkowe informacje debugowania.</span><span class="sxs-lookup"><span data-stu-id="2a655-159">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="2a655-160">Użyj narzędzia do śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="2a655-160">Use a network trace tool to read this code, the error type, and additional parameters.</span></span> <span data-ttu-id="2a655-161">Aby uzyskać pełną listę, zobacz [kody błędów](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="2a655-161">For a full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example-for-microsoft-azure-ms-azr-0145p-subscriptions"></a><span data-ttu-id="2a655-162">Przykład odpowiedzi dla subskrypcji Microsoft Azure (MS-AZR-0145P)</span><span class="sxs-lookup"><span data-stu-id="2a655-162">Response example for Microsoft Azure (MS-AZR-0145P) subscriptions</span></span>

<span data-ttu-id="2a655-163">W tym przykładzie klient zakupił ofertę **145Pą platformy Azure** .</span><span class="sxs-lookup"><span data-stu-id="2a655-163">In this example, the customer purchased a **145P Azure PayG** offer.</span></span>

<span data-ttu-id="2a655-164">*W przypadku klientów z subskrypcjami Microsoft Azure (MS-AZR-0145P) nie będzie zmieniana odpowiedź interfejsu API.*</span><span class="sxs-lookup"><span data-stu-id="2a655-164">*For customers with Microsoft Azure (MS-AZR-0145P) subscriptions, there will be no change to the API response.*</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 1120
Content-Type: application/json
MS-CorrelationId: 47c36033-af5d-4457-80a4-512c1626fac4
MS-RequestId: e128c8e2-4c33-4940-a3e2-2e59b0abdc67
Date: Tue, 17 Sep 2019 20:31:45 GMT

{
    "resourceId": "ABCDEFGH-F347-41B6-B02C-187B1B778A43",
    "id": "ABCDEFGH-F347-41B6-B02C-187B1B778A43",
    "resourceName": "Microsoft Azure",
    "name": "Microsoft Azure",
    "billingStartDate": "2019-08-28T00:00:00-07:00",
    "billingEndDate": "2019-09-27T00:00:00-07:00",
    "totalCost": 22.861172,
    "currencyLocale": "fr-FR",
    "lastModifiedDate": "2019-09-01T23:04:41.193+00:00",
    "links": {
        "self": {
            "uri": "/customers/<customer-tenant-id>/subscriptions/<subscription-id>/usagesummary",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "SubscriptionUsageSummary"
    }
}
```

## <a name="rest-response-example-for-azure-plan"></a><span data-ttu-id="2a655-165">Przykład odpowiedzi REST dla usługi Azure plan</span><span class="sxs-lookup"><span data-stu-id="2a655-165">REST response example for Azure plan</span></span>

<span data-ttu-id="2a655-166">W tym przykładzie klient kupił plan platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="2a655-166">In this example, the customer purchased an Azure plan.</span></span>

<span data-ttu-id="2a655-167">*W przypadku klientów z planami platformy Azure istnieją następujące zmiany dotyczące odpowiedzi interfejsu API:*</span><span class="sxs-lookup"><span data-stu-id="2a655-167">*For customers with Azure plans, there are the following API response changes:*</span></span>

- <span data-ttu-id="2a655-168">**currencyLocale** został zastąpiony **CurrencyCode**</span><span class="sxs-lookup"><span data-stu-id="2a655-168">**currencyLocale** is replaced with **currencyCode**</span></span>
- <span data-ttu-id="2a655-169">**usdTotalCost** jest nowym polem</span><span class="sxs-lookup"><span data-stu-id="2a655-169">**usdTotalCost** is a new field</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 1120
Content-Type: application/json
MS-CorrelationId: 47c36033-af5d-4457-80a4-512c1626fac1
MS-RequestId: e128c8e2-4c33-4940-a3e2-2e59b0abdc67
Date: Tue, 17 Sep 2019 20:31:45 GMT

{
    "resourceId": "11111111-dca5-6f31-d3a6-dbbfad9be0fc",
    "resourceName": "Azure plan",
    "billingStartDate": "2019-09-01T00:00:00+00:00",
    "billingEndDate": "2019-10-01T00:00:00+00:00",
    "totalCost": 28.82860766744404945074,
    "currencyCode": "GBP",
    "usdTotalCost": 35.23000000000000362337,
    "lastModifiedDate": "2019-09-18T17:09:26.16+00:00",
    "links": {
        "self": {
            "uri": "/customers/<customer-tenant-id>/subscriptions/<subscription-id>/usagesummary",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "SubscriptionUsageSummary"
    }
}
```
