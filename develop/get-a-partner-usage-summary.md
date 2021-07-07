---
title: Uzyskiwanie podsumowania użycia dla partnera
description: Możesz użyć zasobu PartnerUsageSummary, aby uzyskać podsumowanie użycia partnera dla wszystkich klientów, którzy kupili określoną usługę lub zasób platformy Azure w bieżącym okresie rozliczeniowym.
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: khpavan
ms.author: sakhanda
ms.openlocfilehash: f003980f1b521ad0ac26dbfd0d4821b9096fdd27
ms.sourcegitcommit: b1d6fd0ca93d8a3e30e970844d3164454415f553
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/09/2021
ms.locfileid: "111873908"
---
# <a name="get-a-usage-summary-for-a-partner"></a><span data-ttu-id="b530f-103">Uzyskiwanie podsumowania użycia dla partnera</span><span class="sxs-lookup"><span data-stu-id="b530f-103">Get a usage summary for a partner</span></span>

<span data-ttu-id="b530f-104">**Dotyczy:** Partner Center | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="b530f-104">**Applies to**: Partner Center | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="b530f-105">Możesz użyć zasobu **PartnerUsageSummary,** aby uzyskać podsumowanie użycia partnera dla wszystkich klientów, którzy kupili określoną usługę lub zasób platformy Azure w bieżącym okresie rozliczeniowym.</span><span class="sxs-lookup"><span data-stu-id="b530f-105">You can use the **PartnerUsageSummary** resource to get a partner usage summary of all customers that purchased a specific Azure service or resource during the current billing period.</span></span>

<span data-ttu-id="b530f-106">*Suma zwrócona przez ten interfejs API nie zwróci zużycia dla klientów, którzy mają plan platformy Azure.*</span><span class="sxs-lookup"><span data-stu-id="b530f-106">*The total returned by this API will not return consumption for customers that have an Azure plan.*</span></span> <span data-ttu-id="b530f-107">Planowane do cofania w przyszłości.</span><span class="sxs-lookup"><span data-stu-id="b530f-107">Planned for deprecation in the future.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b530f-108">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="b530f-108">Prerequisites</span></span>

- <span data-ttu-id="b530f-109">Poświadczenia zgodnie z opisem w te [Partner Center uwierzytelniania.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="b530f-109">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="b530f-110">Ten scenariusz obsługuje uwierzytelnianie tylko przy użyciu poświadczeń aplikacji i użytkownika.</span><span class="sxs-lookup"><span data-stu-id="b530f-110">This scenario supports authentication with App+User credentials only.</span></span>

## <a name="c"></a><span data-ttu-id="b530f-111">C\#</span><span class="sxs-lookup"><span data-stu-id="b530f-111">C\#</span></span>

<span data-ttu-id="b530f-112">Aby uzyskać podsumowanie użycia dla wszystkich klientów, którzy kupili określoną usługę lub zasób platformy Azure w bieżącym okresie rozliczeniowym:</span><span class="sxs-lookup"><span data-stu-id="b530f-112">To get a usage summary for all customers that purchased a specific Azure service or resource during the current billing period:</span></span>

1. <span data-ttu-id="b530f-113">Użyj swojego **konta IAggregatePartner.**</span><span class="sxs-lookup"><span data-stu-id="b530f-113">Use your **IAggregatePartner**.</span></span>

2. <span data-ttu-id="b530f-114">Wywołaj **właściwość UsageSummary,** a następnie metody **Get()** **lub GetAsync():**</span><span class="sxs-lookup"><span data-stu-id="b530f-114">Call the **UsageSummary** property, followed by the **Get()** or **GetAsync()** methods:</span></span>

    ``` csharp
    // IAggregatePartner partnerOperations;

    var usageSummary = partnerOperations.UsageSummary.Get();
    ```

<span data-ttu-id="b530f-115">Przykład można znaleźć w następujących tematach:</span><span class="sxs-lookup"><span data-stu-id="b530f-115">For an example, see the following:</span></span>

- <span data-ttu-id="b530f-116">Przykład: [aplikacja testowa konsoli](console-test-app.md)</span><span class="sxs-lookup"><span data-stu-id="b530f-116">Sample: [Console test app](console-test-app.md)</span></span>
- <span data-ttu-id="b530f-117">Project: **PartnerSDK.FeatureSamples**</span><span class="sxs-lookup"><span data-stu-id="b530f-117">Project: **PartnerSDK.FeatureSamples**</span></span>
- <span data-ttu-id="b530f-118">Klasa: **GetPartnerUsageSummary.cs**</span><span class="sxs-lookup"><span data-stu-id="b530f-118">Class: **GetPartnerUsageSummary.cs**</span></span>

## <a name="rest-request"></a><span data-ttu-id="b530f-119">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="b530f-119">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="b530f-120">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="b530f-120">Request syntax</span></span>

| <span data-ttu-id="b530f-121">Metoda</span><span class="sxs-lookup"><span data-stu-id="b530f-121">Method</span></span>  | <span data-ttu-id="b530f-122">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="b530f-122">Request URI</span></span>                                                         |
|---------|---------------------------------------------------------------------|
| <span data-ttu-id="b530f-123">**Pobierz**</span><span class="sxs-lookup"><span data-stu-id="b530f-123">**GET**</span></span> | <span data-ttu-id="b530f-124">[*{baseURL}*](partner-center-rest-urls.md)/v1/usagesummary HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="b530f-124">[*{baseURL}*](partner-center-rest-urls.md)/v1/usagesummary HTTP/1.1</span></span> |

### <a name="request-headers"></a><span data-ttu-id="b530f-125">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="b530f-125">Request headers</span></span>

<span data-ttu-id="b530f-126">Aby uzyskać więcej informacji, [zobacz Partner Center REST headers (Nagłówki REST).](headers.md)</span><span class="sxs-lookup"><span data-stu-id="b530f-126">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="b530f-127">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="b530f-127">Request body</span></span>

<span data-ttu-id="b530f-128">Brak.</span><span class="sxs-lookup"><span data-stu-id="b530f-128">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="b530f-129">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="b530f-129">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/usagesummary HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: e128c8e2-4c33-4940-a3e2-2e59b0abdc67
MS-CorrelationId: 47c36033-af5d-4457-80a4-512c1626fac4
```

## <a name="rest-response"></a><span data-ttu-id="b530f-130">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="b530f-130">REST response</span></span>

<span data-ttu-id="b530f-131">W przypadku powodzenia ta metoda zwraca **zasób PartnerUsageSummary** w treści odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="b530f-131">If successful, this method returns a **PartnerUsageSummary** resource in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="b530f-132">Kody powodzenia i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="b530f-132">Response success and error codes</span></span>

<span data-ttu-id="b530f-133">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie, oraz dodatkowe informacje o debugowaniu.</span><span class="sxs-lookup"><span data-stu-id="b530f-133">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="b530f-134">Użyj narzędzia śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="b530f-134">Use a network trace tool to read this code, the error type, and additional parameters.</span></span> <span data-ttu-id="b530f-135">Aby uzyskać pełną listę, zobacz [Kody błędów](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="b530f-135">For a full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="b530f-136">Przykład odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="b530f-136">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 1120
Content-Type: application/json
MS-CorrelationId: 47c36033-af5d-4457-80a4-512c1626fac4
MS-RequestId: e128c8e2-4c33-4940-a3e2-2e59b0abdc67
Date: Tue, 17 Sep 2019 20:31:45 GMT

{
    "customersOverBudget": 1,
    "customersTrendingOver": 0,
    "customersWithUsageBasedSubscription": 11,
    "resourceId": "11111111-4574-4539-bc42-0e539b9684c0",
    "id": "11111111-4574-4539-bc42-0e539b9684c0",
    "resourceName": "PLAMUATT2NETNEW",
    "name": "PLAMUATT2NETNEW",
    "billingStartDate": "2019-08-28T00:00:00-07:00",
    "billingEndDate": "2019-09-27T00:00:00-07:00",
    "totalCost": 22.861172,
    "currencyLocale": "fr-FR",
    "lastModifiedDate": "2019-09-01T23:04:41.193+00:00",
    "links": {
        "self": {
            "uri": "/usagesummary",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "PartnerUsageSummary"
    }
}
```
