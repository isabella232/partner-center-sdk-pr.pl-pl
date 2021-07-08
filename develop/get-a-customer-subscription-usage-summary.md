---
title: Uzyskiwanie podsumowania użycia dla subskrypcji klienta
description: Możesz użyć zasobu SubscriptionUsageSummary, aby uzyskać podsumowanie użycia subskrypcji określonej usługi lub zasobu platformy Azure w bieżącym okresie rozliczeniowym.
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 362e72e1b54a62a114564d4dc48a082bcdeea012
ms.sourcegitcommit: b1d6fd0ca93d8a3e30e970844d3164454415f553
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/09/2021
ms.locfileid: "111874673"
---
# <a name="get-usage-summary-for-customers-subscription"></a><span data-ttu-id="6e154-103">Uzyskiwanie podsumowania użycia dla subskrypcji klienta</span><span class="sxs-lookup"><span data-stu-id="6e154-103">Get usage summary for customer's subscription</span></span>

<span data-ttu-id="6e154-104">**Dotyczy:** Partner Center | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="6e154-104">**Applies to**: Partner Center | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="6e154-105">Możesz użyć zasobu **SubscriptionUsageSummary,** aby uzyskać podsumowanie użycia subskrypcji dla klienta.</span><span class="sxs-lookup"><span data-stu-id="6e154-105">You can use the **SubscriptionUsageSummary** resource to get a subscription usage summary for a customer.</span></span> <span data-ttu-id="6e154-106">Ten zasób reprezentuje podsumowanie użycia subskrypcji określonej usługi lub zasobu platformy Azure w bieżącym okresie rozliczeniowym.</span><span class="sxs-lookup"><span data-stu-id="6e154-106">This resource represents the subscription usage summary of a specific Azure service or resource during the current billing period.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6e154-107">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="6e154-107">Prerequisites</span></span>

- <span data-ttu-id="6e154-108">Poświadczenia zgodnie z opisem w te [Partner Center uwierzytelniania.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="6e154-108">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="6e154-109">Ten scenariusz obsługuje uwierzytelnianie tylko przy użyciu poświadczeń aplikacji i użytkownika.</span><span class="sxs-lookup"><span data-stu-id="6e154-109">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="6e154-110">Identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="6e154-110">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="6e154-111">Jeśli nie znasz identyfikatora klienta, możesz go znaleźć na pulpicie nawigacyjnym Partner Center [nawigacyjnym](https://partner.microsoft.com/dashboard).</span><span class="sxs-lookup"><span data-stu-id="6e154-111">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="6e154-112">Wybierz **pozycję CSP** z Partner Center menu, a następnie pozycję **Klienci.**</span><span class="sxs-lookup"><span data-stu-id="6e154-112">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="6e154-113">Wybierz klienta z listy klientów, a następnie wybierz pozycję **Konto**.</span><span class="sxs-lookup"><span data-stu-id="6e154-113">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="6e154-114">Na stronie Konto klienta odszukaj identyfikator **Microsoft w** **sekcji Informacje o koncie** klienta.</span><span class="sxs-lookup"><span data-stu-id="6e154-114">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="6e154-115">Identyfikator microsoft jest taki sam jak identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="6e154-115">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="6e154-116">Identyfikator subskrypcji</span><span class="sxs-lookup"><span data-stu-id="6e154-116">A subscription identifier</span></span>

## <a name="c"></a><span data-ttu-id="6e154-117">C\#</span><span class="sxs-lookup"><span data-stu-id="6e154-117">C\#</span></span>

<span data-ttu-id="6e154-118">Aby uzyskać podsumowanie użycia subskrypcji dla subskrypcji klienta:</span><span class="sxs-lookup"><span data-stu-id="6e154-118">To get a subscription usage summary for a customer's subscription:</span></span>

1. <span data-ttu-id="6e154-119">Użyj **kolekcji IAggregatePartner.Customers,** aby wywołać **metodę ById().**</span><span class="sxs-lookup"><span data-stu-id="6e154-119">Use your **IAggregatePartner.Customers** collection to call the **ById()** method.</span></span>

2. <span data-ttu-id="6e154-120">Następnie wywołaj właściwość Subscriptions i **właściwość UsageSummary.**</span><span class="sxs-lookup"><span data-stu-id="6e154-120">Then call the Subscriptions property and the **UsageSummary** property.</span></span> <span data-ttu-id="6e154-121">Zakończ, wywołując metody Get() lub GetAsync().</span><span class="sxs-lookup"><span data-stu-id="6e154-121">Finish by calling the Get() or GetAsync() methods.</span></span>

    ``` csharp
    // IAggregatePartner partnerOperations;
    // var selectedCustomerId as string;
    // var selectedSubscriptionId as string;

    var subscriptionUsageSummary = partnerOperations.Customers.ById(selectedCustomerId).Subscriptions.ById(selectedSubscriptionId).UsageSummary.Get();
    ```

<span data-ttu-id="6e154-122">Przykład można znaleźć w następujących tematach:</span><span class="sxs-lookup"><span data-stu-id="6e154-122">For an example, see the following:</span></span>

- <span data-ttu-id="6e154-123">Przykład: [aplikacja testowa konsoli](console-test-app.md)</span><span class="sxs-lookup"><span data-stu-id="6e154-123">Sample: [Console test app](console-test-app.md)</span></span>
- <span data-ttu-id="6e154-124">Project: **PartnerSDK.FeatureSamples**</span><span class="sxs-lookup"><span data-stu-id="6e154-124">Project: **PartnerSDK.FeatureSamples**</span></span>
- <span data-ttu-id="6e154-125">Klasa: **GetSubscriptionUsageSummary.cs**</span><span class="sxs-lookup"><span data-stu-id="6e154-125">Class: **GetSubscriptionUsageSummary.cs**</span></span>

## <a name="rest-request"></a><span data-ttu-id="6e154-126">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="6e154-126">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="6e154-127">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="6e154-127">Request syntax</span></span>

| <span data-ttu-id="6e154-128">Metoda</span><span class="sxs-lookup"><span data-stu-id="6e154-128">Method</span></span>  | <span data-ttu-id="6e154-129">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="6e154-129">Request URI</span></span>                                                                                                                        |
|---------|------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="6e154-130">**Pobierz**</span><span class="sxs-lookup"><span data-stu-id="6e154-130">**GET**</span></span> | <span data-ttu-id="6e154-131">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{identyfikator-dzierżawy-klienta}/subscriptions/{subscription-id}/usagesummary HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="6e154-131">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/subscriptions/{subscription-id}/usagesummary HTTP/1.1</span></span> |

#### <a name="uri-parameters"></a><span data-ttu-id="6e154-132">Parametry URI</span><span class="sxs-lookup"><span data-stu-id="6e154-132">URI parameters</span></span>

<span data-ttu-id="6e154-133">W tej tabeli wymieniono wymagane parametry zapytania w celu uzyskania informacji o użyciu ocenionym przez klienta.</span><span class="sxs-lookup"><span data-stu-id="6e154-133">This table lists the required query parameters to get the customer's rated usage information.</span></span>

| <span data-ttu-id="6e154-134">Nazwa</span><span class="sxs-lookup"><span data-stu-id="6e154-134">Name</span></span>                   | <span data-ttu-id="6e154-135">Typ</span><span class="sxs-lookup"><span data-stu-id="6e154-135">Type</span></span>     | <span data-ttu-id="6e154-136">Wymagane</span><span class="sxs-lookup"><span data-stu-id="6e154-136">Required</span></span> | <span data-ttu-id="6e154-137">Opis</span><span class="sxs-lookup"><span data-stu-id="6e154-137">Description</span></span>                               |
|------------------------|----------|----------|-------------------------------------------|
| <span data-ttu-id="6e154-138">**identyfikator dzierżawy klienta**</span><span class="sxs-lookup"><span data-stu-id="6e154-138">**customer-tenant-id**</span></span> | <span data-ttu-id="6e154-139">**guid**</span><span class="sxs-lookup"><span data-stu-id="6e154-139">**guid**</span></span> | <span data-ttu-id="6e154-140">Y</span><span class="sxs-lookup"><span data-stu-id="6e154-140">Y</span></span>        | <span data-ttu-id="6e154-141">Identyfikator GUID odpowiadający klientowi.</span><span class="sxs-lookup"><span data-stu-id="6e154-141">A GUID corresponding to the customer.</span></span>     |
| <span data-ttu-id="6e154-142">**subscription-id**</span><span class="sxs-lookup"><span data-stu-id="6e154-142">**subscription-id**</span></span>    | <span data-ttu-id="6e154-143">**guid**</span><span class="sxs-lookup"><span data-stu-id="6e154-143">**guid**</span></span> | <span data-ttu-id="6e154-144">Y</span><span class="sxs-lookup"><span data-stu-id="6e154-144">Y</span></span>        | <span data-ttu-id="6e154-145">Identyfikator GUID odpowiadający identyfikatorowi subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="6e154-145">A GUID corresponding to the identifier of a subscription.</span></span> <span data-ttu-id="6e154-146">W przypadku planu platformy Azure jest to identyfikator odpowiedniego zasobu Partner Center [subskrypcji](subscription-resources.md#subscription), który reprezentuje plan platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="6e154-146">For an Azure plan, this is the identifier of the corresponding Partner Center [subscription resource](subscription-resources.md#subscription), which represents the Azure plan.</span></span> <span data-ttu-id="6e154-147">*W przypadku zasobów subskrypcji planu platformy Azure podaj **identyfikator planu** jako **subscription-id** w tej trasie.*</span><span class="sxs-lookup"><span data-stu-id="6e154-147">*For Azure plan subscription resources, provide the **plan-id** as the **subscription-id** in this route.*</span></span> |

### <a name="request-headers"></a><span data-ttu-id="6e154-148">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="6e154-148">Request headers</span></span>

<span data-ttu-id="6e154-149">Aby uzyskać więcej informacji, [zobacz Partner Center REST headers (Nagłówki REST).](headers.md)</span><span class="sxs-lookup"><span data-stu-id="6e154-149">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="6e154-150">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="6e154-150">Request body</span></span>

<span data-ttu-id="6e154-151">Brak.</span><span class="sxs-lookup"><span data-stu-id="6e154-151">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="6e154-152">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="6e154-152">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/{customer-tenant-id}/subscriptions/{subscription-id}/usagesummary HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: e128c8e2-4c33-4940-a3e2-2e59b0abdc67
MS-CorrelationId: 47c36033-af5d-4457-80a4-512c1626fac4
```

## <a name="rest-response"></a><span data-ttu-id="6e154-153">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="6e154-153">REST response</span></span>

<span data-ttu-id="6e154-154">W przypadku powodzenia ta metoda zwraca **zasób SubscriptionUsageSummary** w treści odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="6e154-154">If successful, this method returns a **SubscriptionUsageSummary** resource in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="6e154-155">Kody powodzenia i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="6e154-155">Response success and error codes</span></span>

<span data-ttu-id="6e154-156">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie, oraz dodatkowe informacje o debugowaniu.</span><span class="sxs-lookup"><span data-stu-id="6e154-156">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="6e154-157">Użyj narzędzia śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="6e154-157">Use a network trace tool to read this code, the error type, and additional parameters.</span></span> <span data-ttu-id="6e154-158">Aby uzyskać pełną listę, zobacz [Kody błędów](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="6e154-158">For a full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example-for-microsoft-azure-ms-azr-0145p-subscriptions"></a><span data-ttu-id="6e154-159">Przykład odpowiedzi dla Microsoft Azure subskrypcji (MS-AZR-0145P)</span><span class="sxs-lookup"><span data-stu-id="6e154-159">Response example for Microsoft Azure (MS-AZR-0145P) subscriptions</span></span>

<span data-ttu-id="6e154-160">W tym przykładzie klient kupił ofertę **Azure PayG 145P.**</span><span class="sxs-lookup"><span data-stu-id="6e154-160">In this example, the customer purchased a **145P Azure PayG** offer.</span></span>

<span data-ttu-id="6e154-161">*W przypadku klientów Microsoft Azure subskrypcji interfejsu API (MS-AZR-0145P) nie ma żadnych zmian w odpowiedzi interfejsu API.*</span><span class="sxs-lookup"><span data-stu-id="6e154-161">*For customers with Microsoft Azure (MS-AZR-0145P) subscriptions, there will be no change to the API response.*</span></span>

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

## <a name="rest-response-example-for-azure-plan"></a><span data-ttu-id="6e154-162">Przykład odpowiedzi REST dla planu platformy Azure</span><span class="sxs-lookup"><span data-stu-id="6e154-162">REST response example for Azure plan</span></span>

<span data-ttu-id="6e154-163">W tym przykładzie klient kupił plan platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="6e154-163">In this example, the customer purchased an Azure plan.</span></span>

<span data-ttu-id="6e154-164">*W przypadku klientów z planami platformy Azure istnieją następujące zmiany odpowiedzi interfejsu API:*</span><span class="sxs-lookup"><span data-stu-id="6e154-164">*For customers with Azure plans, there are the following API response changes:*</span></span>

- <span data-ttu-id="6e154-165">**CurrencyLocale został** zastąpiony wartością **currencyCode**</span><span class="sxs-lookup"><span data-stu-id="6e154-165">**currencyLocale** is replaced with **currencyCode**</span></span>
- <span data-ttu-id="6e154-166">**USDTotalCost** to nowe pole</span><span class="sxs-lookup"><span data-stu-id="6e154-166">**usdTotalCost** is a new field</span></span>

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
