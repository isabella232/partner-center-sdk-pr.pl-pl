---
title: Pobierz rekordy użycia dla wszystkich klientów
description: Kolekcji zasobów CustomerMonthlyUsageRecord można użyć do uzyskania rekordów użycia dla wszystkich klientów, którzy kupili określoną usługę lub zasób platformy Azure.
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: da829a6de3690a9b1117ce9dfa58fbe381cafd81
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/08/2020
ms.locfileid: "97767981"
---
# <a name="get-usage-records-for-all-customers"></a><span data-ttu-id="e9b27-103">Pobierz rekordy użycia dla wszystkich klientów</span><span class="sxs-lookup"><span data-stu-id="e9b27-103">Get usage records for all customers</span></span>

<span data-ttu-id="e9b27-104">**Dotyczy:**</span><span class="sxs-lookup"><span data-stu-id="e9b27-104">**Applies to:**</span></span>

- <span data-ttu-id="e9b27-105">Centrum partnerskie</span><span class="sxs-lookup"><span data-stu-id="e9b27-105">Partner Center</span></span>
- <span data-ttu-id="e9b27-106">Centrum partnerskie dla Microsoft Cloud Niemcy</span><span class="sxs-lookup"><span data-stu-id="e9b27-106">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="e9b27-107">Centrum partnerskie Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="e9b27-107">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="e9b27-108">Partnerzy mogą używać kolekcji zasobów **CustomerMonthlyUsageRecord** , aby uzyskać rekordy użycia dla wszystkich klientów.</span><span class="sxs-lookup"><span data-stu-id="e9b27-108">Partners can use the **CustomerMonthlyUsageRecord** resource collection to get usage records for all their customers.</span></span> <span data-ttu-id="e9b27-109">Ten zasób reprezentuje rekordy użycia dla wszystkich klientów.</span><span class="sxs-lookup"><span data-stu-id="e9b27-109">This resource represents usage records for all customers.</span></span> <span data-ttu-id="e9b27-110">Obejmuje to klientów z subskrypcją Microsoft Azure (MS-AZR-0145P) lub planem platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="e9b27-110">That includes those customers with a Microsoft Azure (MS-AZR-0145P) subscription or an Azure plan.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e9b27-111">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="e9b27-111">Prerequisites</span></span>

- <span data-ttu-id="e9b27-112">Poświadczenia zgodnie z opisem w temacie [uwierzytelnianie w centrum partnerskim](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="e9b27-112">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="e9b27-113">Ten scenariusz obsługuje tylko uwierzytelnianie przy użyciu aplikacji i poświadczeń użytkownika.</span><span class="sxs-lookup"><span data-stu-id="e9b27-113">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="e9b27-114">Identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="e9b27-114">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="e9b27-115">Jeśli nie znasz identyfikatora klienta, możesz go wyszukać na [pulpicie nawigacyjnym](https://partner.microsoft.com/dashboard)Centrum partnerskiego.</span><span class="sxs-lookup"><span data-stu-id="e9b27-115">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="e9b27-116">Wybierz pozycję **dostawca CSP** z menu Centrum partnerskiego, po którym znajdują się **klienci**.</span><span class="sxs-lookup"><span data-stu-id="e9b27-116">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="e9b27-117">Wybierz klienta z listy klient, a następnie wybierz pozycję **konto**.</span><span class="sxs-lookup"><span data-stu-id="e9b27-117">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="e9b27-118">Na stronie konto klienta Znajdź **Identyfikator Microsoft** w sekcji **Informacje o koncie klienta** .</span><span class="sxs-lookup"><span data-stu-id="e9b27-118">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="e9b27-119">Identyfikator Microsoft jest taki sam jak identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="e9b27-119">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="c"></a><span data-ttu-id="e9b27-120">C\#</span><span class="sxs-lookup"><span data-stu-id="e9b27-120">C\#</span></span>

<span data-ttu-id="e9b27-121">Aby uzyskać wszystkie rekordy użycia dla wszystkich klientów, którzy kupili określoną usługę lub zasób platformy Azure w bieżącym okresie rozliczeniowym:</span><span class="sxs-lookup"><span data-stu-id="e9b27-121">To get all the usage records for all customers who purchased a specific Azure service or resource during the current billing period:</span></span>

1. <span data-ttu-id="e9b27-122">Użyj kolekcji **IAggregatePartner. Customers** , aby wywołać metodę **ById ()** .</span><span class="sxs-lookup"><span data-stu-id="e9b27-122">Use your **IAggregatePartner.Customers** collection to call the **ById()** method.</span></span>

2. <span data-ttu-id="e9b27-123">Wywołaj Właściwość **UsageRecords** , a następnie Wywołaj metodę **Get ()** lub **GetAsync ()** .</span><span class="sxs-lookup"><span data-stu-id="e9b27-123">Call **UsageRecords** property, then call the **Get()** or **GetAsync()** method.</span></span>

    ``` csharp
    // IAggregatePartner partnerOperations;
    var usageRecords = partnerOperations.Customers.UsageRecords.Get();
    ```

<span data-ttu-id="e9b27-124">Aby zapoznać się z przykładem, zobacz następujący przykład:</span><span class="sxs-lookup"><span data-stu-id="e9b27-124">For an example, see the following sample:</span></span>

- <span data-ttu-id="e9b27-125">Przykład: [aplikacja testowa konsoli](console-test-app.md)</span><span class="sxs-lookup"><span data-stu-id="e9b27-125">Sample: [Console test app](console-test-app.md)</span></span>
- <span data-ttu-id="e9b27-126">Projekt: **PartnerSDK. FeatureSamples**</span><span class="sxs-lookup"><span data-stu-id="e9b27-126">Project: **PartnerSDK.FeatureSamples**</span></span>
- <span data-ttu-id="e9b27-127">Klasa: **GetCustomerUsageRecords.cs**</span><span class="sxs-lookup"><span data-stu-id="e9b27-127">Class: **GetCustomerUsageRecords.cs**</span></span>

## <a name="rest-request"></a><span data-ttu-id="e9b27-128">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="e9b27-128">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="e9b27-129">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="e9b27-129">Request syntax</span></span>

| <span data-ttu-id="e9b27-130">Metoda</span><span class="sxs-lookup"><span data-stu-id="e9b27-130">Method</span></span>  | <span data-ttu-id="e9b27-131">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="e9b27-131">Request URI</span></span>                                                                   |
|---------|-------------------------------------------------------------------------------|
| <span data-ttu-id="e9b27-132">**Pobierz**</span><span class="sxs-lookup"><span data-stu-id="e9b27-132">**GET**</span></span> | <span data-ttu-id="e9b27-133">[*{baseURL}*](partner-center-rest-urls.md)/V1/Customers/usagerecords http/1.1</span><span class="sxs-lookup"><span data-stu-id="e9b27-133">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/usagerecords HTTP/1.1</span></span> |

### <a name="request-headers"></a><span data-ttu-id="e9b27-134">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="e9b27-134">Request headers</span></span>

<span data-ttu-id="e9b27-135">Aby uzyskać więcej informacji, zobacz [nagłówki REST Centrum partnerskiego](headers.md).</span><span class="sxs-lookup"><span data-stu-id="e9b27-135">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="e9b27-136">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="e9b27-136">Request body</span></span>

<span data-ttu-id="e9b27-137">Brak.</span><span class="sxs-lookup"><span data-stu-id="e9b27-137">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="e9b27-138">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="e9b27-138">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/usagerecords HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: e128c8e2-4c33-4940-a3e2-2e59b0abdc67
MS-CorrelationId: 47c36033-af5d-4457-80a4-512c1626fac4
```

## <a name="rest-response"></a><span data-ttu-id="e9b27-139">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="e9b27-139">REST response</span></span>

<span data-ttu-id="e9b27-140">Jeśli to się powiedzie, metoda zwraca zasób **CustomerMonthlyUsageRecord** w treści odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="e9b27-140">If successful, this method returns a **CustomerMonthlyUsageRecord** resource in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="e9b27-141">Kody sukcesu i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="e9b27-141">Response success and error codes</span></span>

<span data-ttu-id="e9b27-142">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie i dodatkowe informacje debugowania.</span><span class="sxs-lookup"><span data-stu-id="e9b27-142">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="e9b27-143">Użyj narzędzia do śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="e9b27-143">Use a network trace tool to read this code, the error type, and additional parameters.</span></span> <span data-ttu-id="e9b27-144">Aby uzyskać pełną listę, zobacz [kody błędów](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="e9b27-144">For a full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="e9b27-145">Przykład odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="e9b27-145">Response example</span></span>

<span data-ttu-id="e9b27-146">Właściwość **Isupgraded** służy do identyfikowania klientów, którzy mają plan platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="e9b27-146">You can use the **isUpgraded** property to identify customers who have an Azure plan.</span></span> <span data-ttu-id="e9b27-147">Jeśli wartość parametru **Isupgraded** ma wartość **true**, klienci mają plany platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="e9b27-147">If the value for **isUpgraded** is **true**, it means the customers have Azure plans.</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 1120
Content-Type: application/json
MS-CorrelationId: 47c36033-af5d-4457-80a4-512c1626fac4
MS-RequestId: e128c8e2-4c33-4940-a3e2-2e59b0abdc67
Date: Tue, 17 Sep 2019 20:31:45 GMT

{
    "totalCount": 25,
    "items": [
        {
            "budget": {
                "attributes": {
                    "objectType": "SpendingBudget"
                }
            },
            "customerSpendingBudget": {
                "attributes": {
                    "objectType": "SpendingBudget"
                }
            },
            "percentUsed": 0,
            "isUpgraded": false,
            "resourceId": "11111111-1843-4b3b-872f-206e08a08e51",
            "id": "11111111-1843-4b3b-872f-206e08a08e51",
            "resourceName": "LEGACY AZURE CUSTOMER SE",
            "name": "LEGACY AZURE CUSTOMER SE",
            "totalCost": 0,
            "currencyLocale": "fr-FR",
            "usdTotalCost": 0,
            "lastModifiedDate": "2019-08-01T23:00:16.57+00:00",
            "attributes": {
                "objectType": "CustomerMonthlyUsageRecord"
            }
        },
        {
            "budget": {
                "amount": 20,
                "attributes": {
                    "objectType": "SpendingBudget"
                }
            },
            "percentUsed": 602.84,
            "isUpgraded": true,
            "resourceId": "11111111-6fb9-4b05-8f15-b3d72e0596e6",
            "id": "11111111-6fb9-4b05-8f15-b3d72e0596e6",
            "resourceName": "Modern Azure Customer SE",
            "name": "Modern Azure Customer SE",
            "totalCost": 120.5682999999995904716,
            "currencyCode": "SEK",
            "usdTotalCost": 12.39999999999999985235,
            "lastModifiedDate": "2019-09-17T17:08:11.1433333+00:00",
            "attributes": {
                "objectType": "CustomerMonthlyUsageRecord"
            }
        },
        {
            "budget": {
                "attributes": {
                    "objectType": "SpendingBudget"
                }
            },
            "percentUsed": 0,
            "isUpgraded": true,
            "resourceId": "11111111-5892-4326-8541-9da1fdb233fb",
            "id": "11111111-5892-4326-8541-9da1fdb233fb",
            "resourceName": "Test_Test_MA20190829_14",
            "name": "Test_Test_MA20190829_14",
            "totalCost": 0,
            "currencyCode": "GBP",
            "usdTotalCost": 0,
            "lastModifiedDate": "2019-09-17T17:08:11.1433333+00:00",
            "attributes": {
                "objectType": "CustomerMonthlyUsageRecord"
            }
        },
           {
            "budget": {
                "amount": 97,
                "attributes": {
                    "objectType": "SpendingBudget"
                }
            },
            "percentUsed": 28.08,
            "isUpgraded": true,
            "resourceId": "11111111-641b-4c53-b7fc-0f2bfca8a581",
            "id": "11111111-641b-4c53-b7fc-0f2bfca8a581",
            "resourceName": "Modern Azure Customer UK",
            "name": "Modern Azure Customer UK",
            "totalCost": 27.23292827625710931604,
            "currencyCode": "GBP",
            "usdTotalCost": 33.280000000000001044,
            "lastModifiedDate": "2019-09-17T17:08:11.1433333+00:00",
            "attributes": {
                "objectType": "CustomerMonthlyUsageRecord"
            }
        }
    ],
    "links": {
        "self": {
            "uri": "/customers/usagerecords",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "Collection"
    }
}
```
