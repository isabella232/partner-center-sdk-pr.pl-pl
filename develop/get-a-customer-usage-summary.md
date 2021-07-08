---
title: Uzyskiwanie podsumowania użycia dla wszystkich subskrypcji klienta
description: Możesz użyć zasobu CustomerUsageSummary, aby uzyskać informacje o użyciu określonej usługi lub zasobu platformy Azure przez klienta w bieżącym okresie rozliczeniowym.
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 88c69637c94b9263ede6924cf2dd09513aa00f70
ms.sourcegitcommit: b1d6fd0ca93d8a3e30e970844d3164454415f553
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/09/2021
ms.locfileid: "111874622"
---
# <a name="get-a-usage-summary-for-all-of-a-customers-subscriptions"></a><span data-ttu-id="6c73f-103">Uzyskiwanie podsumowania użycia dla wszystkich subskrypcji klienta</span><span class="sxs-lookup"><span data-stu-id="6c73f-103">Get a usage summary for all of a customer's subscriptions</span></span>

<span data-ttu-id="6c73f-104">**Dotyczy:** Partner Center | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="6c73f-104">**Applies to**: Partner Center | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="6c73f-105">Możesz użyć zasobu **CustomerUsageSummary,** aby uzyskać informacje o użyciu określonej usługi lub zasobu platformy Azure przez klienta w bieżącym okresie rozliczeniowym.</span><span class="sxs-lookup"><span data-stu-id="6c73f-105">You can use the **CustomerUsageSummary** resource to get a customer's usage of a specific Azure service or resource during the current billing period.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6c73f-106">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="6c73f-106">Prerequisites</span></span>

- <span data-ttu-id="6c73f-107">Poświadczenia zgodnie z opisem w te [Partner Center uwierzytelniania.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="6c73f-107">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="6c73f-108">Ten scenariusz obsługuje uwierzytelnianie tylko przy użyciu poświadczeń aplikacji i użytkownika.</span><span class="sxs-lookup"><span data-stu-id="6c73f-108">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="6c73f-109">Identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="6c73f-109">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="6c73f-110">Jeśli nie znasz identyfikatora klienta, możesz go znaleźć na pulpicie nawigacyjnym Partner Center [nawigacyjnym](https://partner.microsoft.com/dashboard).</span><span class="sxs-lookup"><span data-stu-id="6c73f-110">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="6c73f-111">Wybierz **pozycję CSP** z Partner Center menu, a następnie pozycję **Klienci.**</span><span class="sxs-lookup"><span data-stu-id="6c73f-111">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="6c73f-112">Wybierz klienta z listy klientów, a następnie wybierz pozycję **Konto**.</span><span class="sxs-lookup"><span data-stu-id="6c73f-112">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="6c73f-113">Na stronie Konto klienta odszukaj identyfikator **Microsoft w** **sekcji Informacje o koncie** klienta.</span><span class="sxs-lookup"><span data-stu-id="6c73f-113">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="6c73f-114">Identyfikator microsoft jest taki sam jak identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="6c73f-114">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="c"></a><span data-ttu-id="6c73f-115">C\#</span><span class="sxs-lookup"><span data-stu-id="6c73f-115">C\#</span></span>

<span data-ttu-id="6c73f-116">Aby uzyskać podsumowanie użycia dla wszystkich subskrypcji klienta:</span><span class="sxs-lookup"><span data-stu-id="6c73f-116">To get a usage summary for all of a customer's subscriptions:</span></span>

1. <span data-ttu-id="6c73f-117">Użyj **kolekcji IAggregatePartner.Customers,** aby wywołać **metodę ById().**</span><span class="sxs-lookup"><span data-stu-id="6c73f-117">Use your **IAggregatePartner.Customers** collection to call the **ById()** method.</span></span>

2. <span data-ttu-id="6c73f-118">Wywołaj **właściwość UsageSummary,** a następnie metody **Get()** **lub GetAsync():**</span><span class="sxs-lookup"><span data-stu-id="6c73f-118">Call the **UsageSummary** property, followed by the **Get()** or **GetAsync()** methods:</span></span>

    ``` csharp
    // IAggregatePartner partnerOperations;
    // var selectedCustomerId as string;

    var usageSummary = partnerOperations.Customers.ById(selectedCustomerId).UsageSummary.Get();
    ```

<span data-ttu-id="6c73f-119">Przykład można znaleźć w następujących tematach:</span><span class="sxs-lookup"><span data-stu-id="6c73f-119">For an example, see the following:</span></span>

- <span data-ttu-id="6c73f-120">Przykład: [aplikacja testowa konsoli](console-test-app.md)</span><span class="sxs-lookup"><span data-stu-id="6c73f-120">Sample: [Console test app](console-test-app.md)</span></span>
- <span data-ttu-id="6c73f-121">Project: **PartnerSDK.FeatureSamples**</span><span class="sxs-lookup"><span data-stu-id="6c73f-121">Project: **PartnerSDK.FeatureSamples**</span></span>
- <span data-ttu-id="6c73f-122">Klasa: **GetCustomerUsageSummary.cs**</span><span class="sxs-lookup"><span data-stu-id="6c73f-122">Class: **GetCustomerUsageSummary.cs**</span></span>

## <a name="rest-request"></a><span data-ttu-id="6c73f-123">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="6c73f-123">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="6c73f-124">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="6c73f-124">Request syntax</span></span>

| <span data-ttu-id="6c73f-125">Metoda</span><span class="sxs-lookup"><span data-stu-id="6c73f-125">Method</span></span>  | <span data-ttu-id="6c73f-126">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="6c73f-126">Request URI</span></span>                                                                                         |
|---------|-----------------------------------------------------------------------------------------------------|
| <span data-ttu-id="6c73f-127">**Pobierz**</span><span class="sxs-lookup"><span data-stu-id="6c73f-127">**GET**</span></span> | <span data-ttu-id="6c73f-128">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{identyfikator-dzierżawy-klienta}/usagesummary HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="6c73f-128">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/usagesummary HTTP/1.1</span></span> |

#### <a name="uri-parameter"></a><span data-ttu-id="6c73f-129">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="6c73f-129">URI parameter</span></span>

<span data-ttu-id="6c73f-130">W tej tabeli wymieniono wymagany parametr zapytania w celu uzyskania informacji o użyciu ocenionym przez klienta.</span><span class="sxs-lookup"><span data-stu-id="6c73f-130">This table lists the required query parameter to get the customer's rated usage information.</span></span>

| <span data-ttu-id="6c73f-131">Nazwa</span><span class="sxs-lookup"><span data-stu-id="6c73f-131">Name</span></span>                   | <span data-ttu-id="6c73f-132">Typ</span><span class="sxs-lookup"><span data-stu-id="6c73f-132">Type</span></span>     | <span data-ttu-id="6c73f-133">Wymagane</span><span class="sxs-lookup"><span data-stu-id="6c73f-133">Required</span></span> | <span data-ttu-id="6c73f-134">Opis</span><span class="sxs-lookup"><span data-stu-id="6c73f-134">Description</span></span>                           |
|------------------------|----------|----------|---------------------------------------|
| <span data-ttu-id="6c73f-135">**identyfikator dzierżawy klienta**</span><span class="sxs-lookup"><span data-stu-id="6c73f-135">**customer-tenant-id**</span></span> | <span data-ttu-id="6c73f-136">**guid**</span><span class="sxs-lookup"><span data-stu-id="6c73f-136">**guid**</span></span> | <span data-ttu-id="6c73f-137">Y</span><span class="sxs-lookup"><span data-stu-id="6c73f-137">Y</span></span>        | <span data-ttu-id="6c73f-138">Identyfikator GUID odpowiadający klientowi.</span><span class="sxs-lookup"><span data-stu-id="6c73f-138">A GUID corresponding to the customer.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="6c73f-139">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="6c73f-139">Request headers</span></span>

<span data-ttu-id="6c73f-140">Aby uzyskać więcej informacji, [zobacz Partner Center REST headers (Nagłówki REST).](headers.md)</span><span class="sxs-lookup"><span data-stu-id="6c73f-140">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="6c73f-141">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="6c73f-141">Request body</span></span>

<span data-ttu-id="6c73f-142">Brak.</span><span class="sxs-lookup"><span data-stu-id="6c73f-142">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="6c73f-143">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="6c73f-143">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/{customer-tenant-id}/usagesummary HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: e128c8e2-4c33-4940-a3e2-2e59b0abdc67
MS-CorrelationId: 47c36033-af5d-4457-80a4-512c1626fac4
```

## <a name="rest-response"></a><span data-ttu-id="6c73f-144">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="6c73f-144">REST response</span></span>

<span data-ttu-id="6c73f-145">W przypadku powodzenia ta metoda zwraca **zasób CustomerUsageSummary** w treści odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="6c73f-145">If successful, this method returns a **CustomerUsageSummary** resource in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="6c73f-146">Kody powodzenia i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="6c73f-146">Response success and error codes</span></span>

<span data-ttu-id="6c73f-147">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie, oraz dodatkowe informacje o debugowaniu.</span><span class="sxs-lookup"><span data-stu-id="6c73f-147">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="6c73f-148">Użyj narzędzia śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="6c73f-148">Use a network trace tool to read this code, the error type, and additional parameters.</span></span> <span data-ttu-id="6c73f-149">Aby uzyskać pełną listę, zobacz [Kody błędów](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="6c73f-149">For a full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example-for-microsoft-azure-ms-azr-0145p-subscription"></a><span data-ttu-id="6c73f-150">Przykład odpowiedzi dla Microsoft Azure subskrypcji (MS-AZR-0145P)</span><span class="sxs-lookup"><span data-stu-id="6c73f-150">Response example for Microsoft Azure (MS-AZR-0145P) subscription</span></span>

<span data-ttu-id="6c73f-151">W tym przykładzie klient kupił ofertę **Azure PayG 145P.**</span><span class="sxs-lookup"><span data-stu-id="6c73f-151">In this example, the customer purchased a **145P Azure PayG** offer.</span></span>

<span data-ttu-id="6c73f-152">*W przypadku klientów Microsoft Azure subskrypcji interfejsu API (MS-AZR-0145P) nie ma żadnych zmian w odpowiedzi interfejsu API.*</span><span class="sxs-lookup"><span data-stu-id="6c73f-152">*For customers with Microsoft Azure (MS-AZR-0145P) subscriptions, there will be no change to the API response.*</span></span>

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

### <a name="response-example-for-azure-plan"></a><span data-ttu-id="6c73f-153">Przykład odpowiedzi dla planu platformy Azure</span><span class="sxs-lookup"><span data-stu-id="6c73f-153">Response example for Azure plan</span></span>

<span data-ttu-id="6c73f-154">W tym przykładzie klient kupił plan platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="6c73f-154">In this example, the customer purchased an Azure plan.</span></span>

<span data-ttu-id="6c73f-155">*W przypadku klientów z planami platformy Azure istnieją następujące zmiany odpowiedzi interfejsu API:*</span><span class="sxs-lookup"><span data-stu-id="6c73f-155">*For customers with Azure plans, there are the following changes to the API response:*</span></span>

- <span data-ttu-id="6c73f-156">**CurrencyLocale został** zastąpiony wartością **currencyCode**</span><span class="sxs-lookup"><span data-stu-id="6c73f-156">**currencyLocale** is replaced with **currencyCode**</span></span>
- <span data-ttu-id="6c73f-157">**USDTotalCost** to nowe pole</span><span class="sxs-lookup"><span data-stu-id="6c73f-157">**usdTotalCost** is a new field</span></span>

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
