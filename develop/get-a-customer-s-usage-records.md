---
title: Uzyskiwanie rekordów użycia dla wszystkich klientów
description: Kolekcji zasobów CustomerMonthlyUsageRecord można użyć do pobierania rekordów użycia dla wszystkich klientów, którzy kupili określoną usługę lub zasób platformy Azure.
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 6b3fb0e1989336810f2afcc2a5bfc3a1d2849b7f
ms.sourcegitcommit: b1d6fd0ca93d8a3e30e970844d3164454415f553
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/09/2021
ms.locfileid: "111874894"
---
# <a name="get-usage-records-for-all-customers"></a><span data-ttu-id="72629-103">Uzyskiwanie rekordów użycia dla wszystkich klientów</span><span class="sxs-lookup"><span data-stu-id="72629-103">Get usage records for all customers</span></span>

<span data-ttu-id="72629-104">**Dotyczy:** Partner Center | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="72629-104">**Applies to**: Partner Center | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="72629-105">Partnerzy mogą używać **kolekcji zasobów CustomerMonthlyUsageRecord,** aby uzyskać rekordy użycia dla wszystkich swoich klientów.</span><span class="sxs-lookup"><span data-stu-id="72629-105">Partners can use the **CustomerMonthlyUsageRecord** resource collection to get usage records for all their customers.</span></span> <span data-ttu-id="72629-106">Ten zasób reprezentuje rekordy użycia dla wszystkich klientów.</span><span class="sxs-lookup"><span data-stu-id="72629-106">This resource represents usage records for all customers.</span></span> <span data-ttu-id="72629-107">Dotyczy to również klientów z subskrypcją Microsoft Azure (MS-AZR-0145P) lub planem platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="72629-107">That includes those customers with a Microsoft Azure (MS-AZR-0145P) subscription or an Azure plan.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="72629-108">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="72629-108">Prerequisites</span></span>

- <span data-ttu-id="72629-109">Poświadczenia zgodnie z opisem w te [Partner Center uwierzytelniania.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="72629-109">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="72629-110">Ten scenariusz obsługuje uwierzytelnianie tylko przy użyciu poświadczeń aplikacji i użytkownika.</span><span class="sxs-lookup"><span data-stu-id="72629-110">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="72629-111">Identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="72629-111">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="72629-112">Jeśli nie znasz identyfikatora klienta, możesz go znaleźć na pulpicie nawigacyjnym Partner Center [nawigacyjnym](https://partner.microsoft.com/dashboard).</span><span class="sxs-lookup"><span data-stu-id="72629-112">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="72629-113">Wybierz **pozycję CSP** z Partner Center menu, a następnie pozycję **Klienci.**</span><span class="sxs-lookup"><span data-stu-id="72629-113">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="72629-114">Wybierz klienta z listy klientów, a następnie wybierz pozycję **Konto**.</span><span class="sxs-lookup"><span data-stu-id="72629-114">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="72629-115">Na stronie Konto klienta odszukaj identyfikator **Microsoft w** **sekcji Informacje o koncie** klienta.</span><span class="sxs-lookup"><span data-stu-id="72629-115">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="72629-116">Identyfikator microsoft jest taki sam jak identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="72629-116">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="c"></a><span data-ttu-id="72629-117">C\#</span><span class="sxs-lookup"><span data-stu-id="72629-117">C\#</span></span>

<span data-ttu-id="72629-118">Aby uzyskać wszystkie rekordy użycia dla wszystkich klientów, którzy kupili określoną usługę lub zasób platformy Azure w bieżącym okresie rozliczeniowym:</span><span class="sxs-lookup"><span data-stu-id="72629-118">To get all the usage records for all customers who purchased a specific Azure service or resource during the current billing period:</span></span>

1. <span data-ttu-id="72629-119">Użyj **kolekcji IAggregatePartner.Customers,** aby wywołać **metodę ById().**</span><span class="sxs-lookup"><span data-stu-id="72629-119">Use your **IAggregatePartner.Customers** collection to call the **ById()** method.</span></span>

2. <span data-ttu-id="72629-120">Wywołaj **właściwość UsageRecords,** a następnie wywołaj metodę **Get()** **lub GetAsync().**</span><span class="sxs-lookup"><span data-stu-id="72629-120">Call **UsageRecords** property, then call the **Get()** or **GetAsync()** method.</span></span>

    ``` csharp
    // IAggregatePartner partnerOperations;
    var usageRecords = partnerOperations.Customers.UsageRecords.Get();
    ```

<span data-ttu-id="72629-121">Aby uzyskać przykład, zobacz następujący przykład:</span><span class="sxs-lookup"><span data-stu-id="72629-121">For an example, see the following sample:</span></span>

- <span data-ttu-id="72629-122">Przykład: [aplikacja testowa konsoli](console-test-app.md)</span><span class="sxs-lookup"><span data-stu-id="72629-122">Sample: [Console test app](console-test-app.md)</span></span>
- <span data-ttu-id="72629-123">Project: **PartnerSDK.FeatureSamples**</span><span class="sxs-lookup"><span data-stu-id="72629-123">Project: **PartnerSDK.FeatureSamples**</span></span>
- <span data-ttu-id="72629-124">Klasa: **GetCustomerUsageRecords.cs**</span><span class="sxs-lookup"><span data-stu-id="72629-124">Class: **GetCustomerUsageRecords.cs**</span></span>

## <a name="rest-request"></a><span data-ttu-id="72629-125">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="72629-125">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="72629-126">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="72629-126">Request syntax</span></span>

| <span data-ttu-id="72629-127">Metoda</span><span class="sxs-lookup"><span data-stu-id="72629-127">Method</span></span>  | <span data-ttu-id="72629-128">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="72629-128">Request URI</span></span>                                                                   |
|---------|-------------------------------------------------------------------------------|
| <span data-ttu-id="72629-129">**Pobierz**</span><span class="sxs-lookup"><span data-stu-id="72629-129">**GET**</span></span> | <span data-ttu-id="72629-130">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/usagerecords HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="72629-130">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/usagerecords HTTP/1.1</span></span> |

### <a name="request-headers"></a><span data-ttu-id="72629-131">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="72629-131">Request headers</span></span>

<span data-ttu-id="72629-132">Aby uzyskać więcej informacji, [zobacz Partner Center REST headers (Nagłówki REST).](headers.md)</span><span class="sxs-lookup"><span data-stu-id="72629-132">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="72629-133">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="72629-133">Request body</span></span>

<span data-ttu-id="72629-134">Brak.</span><span class="sxs-lookup"><span data-stu-id="72629-134">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="72629-135">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="72629-135">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/usagerecords HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: e128c8e2-4c33-4940-a3e2-2e59b0abdc67
MS-CorrelationId: 47c36033-af5d-4457-80a4-512c1626fac4
```

## <a name="rest-response"></a><span data-ttu-id="72629-136">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="72629-136">REST response</span></span>

<span data-ttu-id="72629-137">W przypadku powodzenia ta metoda zwraca **zasób CustomerMonthlyUsageRecord** w treści odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="72629-137">If successful, this method returns a **CustomerMonthlyUsageRecord** resource in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="72629-138">Kody powodzenia i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="72629-138">Response success and error codes</span></span>

<span data-ttu-id="72629-139">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie, oraz dodatkowe informacje o debugowaniu.</span><span class="sxs-lookup"><span data-stu-id="72629-139">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="72629-140">Użyj narzędzia śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="72629-140">Use a network trace tool to read this code, the error type, and additional parameters.</span></span> <span data-ttu-id="72629-141">Aby uzyskać pełną listę, zobacz [Kody błędów](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="72629-141">For a full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="72629-142">Przykład odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="72629-142">Response example</span></span>

<span data-ttu-id="72629-143">Możesz użyć właściwości **isUpgraded,** aby zidentyfikować klientów, którzy mają plan platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="72629-143">You can use the **isUpgraded** property to identify customers who have an Azure plan.</span></span> <span data-ttu-id="72629-144">Jeśli wartość właściwości **isUpgraded ma** wartość **true,** oznacza to, że klienci mają plany platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="72629-144">If the value for **isUpgraded** is **true**, it means the customers have Azure plans.</span></span>

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
