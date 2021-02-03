---
title: Pobierz Podsumowanie użycia dla wszystkich subskrypcji klienta
description: Zasobu CustomerUsageSummary można użyć do uzyskania użycia określonej usługi lub zasobu platformy Azure w bieżącym okresie rozliczeniowym.
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 0c918434367a3514e6a6ad6034b4897c33f51025
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/08/2020
ms.locfileid: "97767961"
---
# <a name="get-a-usage-summary-for-all-of-a-customers-subscriptions"></a><span data-ttu-id="fd206-103">Pobierz Podsumowanie użycia dla wszystkich subskrypcji klienta</span><span class="sxs-lookup"><span data-stu-id="fd206-103">Get a usage summary for all of a customer's subscriptions</span></span>

<span data-ttu-id="fd206-104">**Dotyczy:**</span><span class="sxs-lookup"><span data-stu-id="fd206-104">**Applies to:**</span></span>

- <span data-ttu-id="fd206-105">Centrum partnerskie</span><span class="sxs-lookup"><span data-stu-id="fd206-105">Partner Center</span></span>
- <span data-ttu-id="fd206-106">Centrum partnerskie dla Microsoft Cloud Niemcy</span><span class="sxs-lookup"><span data-stu-id="fd206-106">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="fd206-107">Centrum partnerskie Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="fd206-107">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="fd206-108">Zasobu **CustomerUsageSummary** można użyć do uzyskania użycia określonej usługi lub zasobu platformy Azure w bieżącym okresie rozliczeniowym.</span><span class="sxs-lookup"><span data-stu-id="fd206-108">You can use the **CustomerUsageSummary** resource to get a customer's usage of a specific Azure service or resource during the current billing period.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="fd206-109">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="fd206-109">Prerequisites</span></span>

- <span data-ttu-id="fd206-110">Poświadczenia zgodnie z opisem w temacie [uwierzytelnianie w centrum partnerskim](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="fd206-110">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="fd206-111">Ten scenariusz obsługuje tylko uwierzytelnianie przy użyciu aplikacji i poświadczeń użytkownika.</span><span class="sxs-lookup"><span data-stu-id="fd206-111">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="fd206-112">Identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="fd206-112">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="fd206-113">Jeśli nie znasz identyfikatora klienta, możesz go wyszukać na [pulpicie nawigacyjnym](https://partner.microsoft.com/dashboard)Centrum partnerskiego.</span><span class="sxs-lookup"><span data-stu-id="fd206-113">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="fd206-114">Wybierz pozycję **dostawca CSP** z menu Centrum partnerskiego, po którym znajdują się **klienci**.</span><span class="sxs-lookup"><span data-stu-id="fd206-114">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="fd206-115">Wybierz klienta z listy klient, a następnie wybierz pozycję **konto**.</span><span class="sxs-lookup"><span data-stu-id="fd206-115">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="fd206-116">Na stronie konto klienta Znajdź **Identyfikator Microsoft** w sekcji **Informacje o koncie klienta** .</span><span class="sxs-lookup"><span data-stu-id="fd206-116">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="fd206-117">Identyfikator Microsoft jest taki sam jak identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="fd206-117">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="c"></a><span data-ttu-id="fd206-118">C\#</span><span class="sxs-lookup"><span data-stu-id="fd206-118">C\#</span></span>

<span data-ttu-id="fd206-119">Aby uzyskać podsumowanie użycia dla wszystkich subskrypcji klienta:</span><span class="sxs-lookup"><span data-stu-id="fd206-119">To get a usage summary for all of a customer's subscriptions:</span></span>

1. <span data-ttu-id="fd206-120">Użyj kolekcji **IAggregatePartner. Customers** , aby wywołać metodę **ById ()** .</span><span class="sxs-lookup"><span data-stu-id="fd206-120">Use your **IAggregatePartner.Customers** collection to call the **ById()** method.</span></span>

2. <span data-ttu-id="fd206-121">Wywołaj Właściwość **UsageSummary** , a następnie metodę **Get ()** lub **GetAsync ()** :</span><span class="sxs-lookup"><span data-stu-id="fd206-121">Call the **UsageSummary** property, followed by the **Get()** or **GetAsync()** methods:</span></span>

    ``` csharp
    // IAggregatePartner partnerOperations;
    // var selectedCustomerId as string;

    var usageSummary = partnerOperations.Customers.ById(selectedCustomerId).UsageSummary.Get();
    ```

<span data-ttu-id="fd206-122">Aby zapoznać się z przykładem, zobacz następujące tematy:</span><span class="sxs-lookup"><span data-stu-id="fd206-122">For an example, see the following:</span></span>

- <span data-ttu-id="fd206-123">Przykład: [aplikacja testowa konsoli](console-test-app.md)</span><span class="sxs-lookup"><span data-stu-id="fd206-123">Sample: [Console test app](console-test-app.md)</span></span>
- <span data-ttu-id="fd206-124">Projekt: **PartnerSDK. FeatureSamples**</span><span class="sxs-lookup"><span data-stu-id="fd206-124">Project: **PartnerSDK.FeatureSamples**</span></span>
- <span data-ttu-id="fd206-125">Klasa: **GetCustomerUsageSummary.cs**</span><span class="sxs-lookup"><span data-stu-id="fd206-125">Class: **GetCustomerUsageSummary.cs**</span></span>

## <a name="rest-request"></a><span data-ttu-id="fd206-126">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="fd206-126">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="fd206-127">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="fd206-127">Request syntax</span></span>

| <span data-ttu-id="fd206-128">Metoda</span><span class="sxs-lookup"><span data-stu-id="fd206-128">Method</span></span>  | <span data-ttu-id="fd206-129">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="fd206-129">Request URI</span></span>                                                                                         |
|---------|-----------------------------------------------------------------------------------------------------|
| <span data-ttu-id="fd206-130">**Pobierz**</span><span class="sxs-lookup"><span data-stu-id="fd206-130">**GET**</span></span> | <span data-ttu-id="fd206-131">[*{baseURL}*](partner-center-rest-urls.md)/V1/Customers/{Customer-tenant-ID}/usagesummary http/1.1</span><span class="sxs-lookup"><span data-stu-id="fd206-131">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/usagesummary HTTP/1.1</span></span> |

#### <a name="uri-parameter"></a><span data-ttu-id="fd206-132">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="fd206-132">URI parameter</span></span>

<span data-ttu-id="fd206-133">W tej tabeli przedstawiono parametr zapytania wymaganego do uzyskania informacji o znamionowym użyciu klienta.</span><span class="sxs-lookup"><span data-stu-id="fd206-133">This table lists the required query parameter to get the customer's rated usage information.</span></span>

| <span data-ttu-id="fd206-134">Nazwa</span><span class="sxs-lookup"><span data-stu-id="fd206-134">Name</span></span>                   | <span data-ttu-id="fd206-135">Typ</span><span class="sxs-lookup"><span data-stu-id="fd206-135">Type</span></span>     | <span data-ttu-id="fd206-136">Wymagane</span><span class="sxs-lookup"><span data-stu-id="fd206-136">Required</span></span> | <span data-ttu-id="fd206-137">Opis</span><span class="sxs-lookup"><span data-stu-id="fd206-137">Description</span></span>                           |
|------------------------|----------|----------|---------------------------------------|
| <span data-ttu-id="fd206-138">**Identyfikator dzierżawy klienta**</span><span class="sxs-lookup"><span data-stu-id="fd206-138">**customer-tenant-id**</span></span> | <span data-ttu-id="fd206-139">**guid**</span><span class="sxs-lookup"><span data-stu-id="fd206-139">**guid**</span></span> | <span data-ttu-id="fd206-140">Y</span><span class="sxs-lookup"><span data-stu-id="fd206-140">Y</span></span>        | <span data-ttu-id="fd206-141">Identyfikator GUID odpowiadający klientowi.</span><span class="sxs-lookup"><span data-stu-id="fd206-141">A GUID corresponding to the customer.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="fd206-142">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="fd206-142">Request headers</span></span>

<span data-ttu-id="fd206-143">Aby uzyskać więcej informacji, zobacz [nagłówki REST Centrum partnerskiego](headers.md).</span><span class="sxs-lookup"><span data-stu-id="fd206-143">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="fd206-144">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="fd206-144">Request body</span></span>

<span data-ttu-id="fd206-145">Brak.</span><span class="sxs-lookup"><span data-stu-id="fd206-145">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="fd206-146">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="fd206-146">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/{customer-tenant-id}/usagesummary HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: e128c8e2-4c33-4940-a3e2-2e59b0abdc67
MS-CorrelationId: 47c36033-af5d-4457-80a4-512c1626fac4
```

## <a name="rest-response"></a><span data-ttu-id="fd206-147">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="fd206-147">REST response</span></span>

<span data-ttu-id="fd206-148">Jeśli to się powiedzie, metoda zwraca zasób **CustomerUsageSummary** w treści odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="fd206-148">If successful, this method returns a **CustomerUsageSummary** resource in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="fd206-149">Kody sukcesu i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="fd206-149">Response success and error codes</span></span>

<span data-ttu-id="fd206-150">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie i dodatkowe informacje debugowania.</span><span class="sxs-lookup"><span data-stu-id="fd206-150">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="fd206-151">Użyj narzędzia do śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="fd206-151">Use a network trace tool to read this code, the error type, and additional parameters.</span></span> <span data-ttu-id="fd206-152">Aby uzyskać pełną listę, zobacz [kody błędów](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="fd206-152">For a full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example-for-microsoft-azure-ms-azr-0145p-subscription"></a><span data-ttu-id="fd206-153">Przykład odpowiedzi dla subskrypcji Microsoft Azure (MS-AZR-0145P)</span><span class="sxs-lookup"><span data-stu-id="fd206-153">Response example for Microsoft Azure (MS-AZR-0145P) subscription</span></span>

<span data-ttu-id="fd206-154">W tym przykładzie klient zakupił ofertę **145Pą platformy Azure** .</span><span class="sxs-lookup"><span data-stu-id="fd206-154">In this example, the customer purchased a **145P Azure PayG** offer.</span></span>

<span data-ttu-id="fd206-155">*W przypadku klientów z subskrypcjami Microsoft Azure (MS-AZR-0145P) nie będzie zmieniana odpowiedź interfejsu API.*</span><span class="sxs-lookup"><span data-stu-id="fd206-155">*For customers with Microsoft Azure (MS-AZR-0145P) subscriptions, there will be no change to the API response.*</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 1120
Content-Type: application/json
MS-CorrelationId: 47c36033-af5d-4457-80a4-512c1626fac4
MS-RequestId: e128c8e2-4c33-4940-a3e2-2e59b0abdc67
Date: Tue, 17 Sep 2019 20:31:45 GMT

{
    "budget":{
        "ammount":300.000000,
        "attributes":{
            "objectType":"SpendingBudget"
        }
    },
    "id":"65726577-C208-40FD-9735-8C85AC9CAC68",
    "name":"600 test",
    "billingStartDate":"2016-02-06T00:00:00-08:00",
    "billingEndDate":"2016-03-05T00:00:00-08:00",
    "totalCost":0.0,
    "currencyLocale":"en-US",
    "lastModifiedDate":"2016-02-26T09:42:54.5130558+00:00",
    "links":{
        "self":{
            "uri":"/customers/{customer-tenant-id}/usagesummary",
            "method":"GET",
            "headers":[]
        }
    },
    "attributes":{
        "objectType":"CustomerUsageSummary"
    }
}
```

### <a name="response-example-for-azure-plan"></a><span data-ttu-id="fd206-156">Przykład odpowiedzi dla planu platformy Azure</span><span class="sxs-lookup"><span data-stu-id="fd206-156">Response example for Azure plan</span></span>

<span data-ttu-id="fd206-157">W tym przykładzie klient kupił plan platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="fd206-157">In this example, the customer purchased an Azure plan.</span></span>

<span data-ttu-id="fd206-158">*W przypadku klientów z planami platformy Azure w odpowiedzi interfejsu API istnieją następujące zmiany:*</span><span class="sxs-lookup"><span data-stu-id="fd206-158">*For customers with Azure plans, there are the following changes to the API response:*</span></span>

- <span data-ttu-id="fd206-159">**currencyLocale** został zastąpiony **CurrencyCode**</span><span class="sxs-lookup"><span data-stu-id="fd206-159">**currencyLocale** is replaced with **currencyCode**</span></span>
- <span data-ttu-id="fd206-160">**usdTotalCost** jest nowym polem</span><span class="sxs-lookup"><span data-stu-id="fd206-160">**usdTotalCost** is a new field</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 1120
Content-Type: application/json
MS-CorrelationId: 47c36033-af5d-4457-80a4-512c1626fac4
MS-RequestId: e128c8e2-4c33-4940-a3e2-2e59b0abdc67
Date: Tue, 17 Sep 2019 20:31:45 GMT

{
    "budget": {
        "amount": 97,
        "attributes": {
            "objectType": "SpendingBudget"
        }
    },
    "resourceId": "44908a11-641b-4c53-b7fc-0f2bfca8a581",
    "resourceName": "Modern Azure Customer UK",
    "billingStartDate": "2019-09-01T00:00:00+00:00",
    "billingEndDate": "2019-10-01T00:00:00+00:00",
    "totalCost": 28.82860766744404945074,
    "currencyCode": "GBP",
    "usdTotalCost": 35.23000000000000362337,
    "lastModifiedDate": "2019-09-18T17:09:26.16+00:00",
    "attributes": {
        "objectType": "CustomerUsageSummary"
    }
}
```
