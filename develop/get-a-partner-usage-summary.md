---
title: Pobieranie podsumowania użycia dla partnera
description: Zasobu PartnerUsageSummary można użyć do uzyskania podsumowania użycia partnerów dla wszystkich klientów, którzy kupili określoną usługę lub zasób platformy Azure w bieżącym okresie rozliczeniowym.
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: khpavan
ms.author: sakhanda
ms.openlocfilehash: ba1885f46043a75274595239fe61ce3ef0998acf
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/08/2020
ms.locfileid: "97767898"
---
# <a name="get-a-usage-summary-for-a-partner"></a><span data-ttu-id="bd396-103">Pobieranie podsumowania użycia dla partnera</span><span class="sxs-lookup"><span data-stu-id="bd396-103">Get a usage summary for a partner</span></span>

<span data-ttu-id="bd396-104">**Dotyczy:**</span><span class="sxs-lookup"><span data-stu-id="bd396-104">**Applies to:**</span></span>

- <span data-ttu-id="bd396-105">Centrum partnerskie</span><span class="sxs-lookup"><span data-stu-id="bd396-105">Partner Center</span></span>
- <span data-ttu-id="bd396-106">Centrum partnerskie dla Microsoft Cloud Niemcy</span><span class="sxs-lookup"><span data-stu-id="bd396-106">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="bd396-107">Centrum partnerskie Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="bd396-107">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="bd396-108">Zasobu **PartnerUsageSummary** można użyć do uzyskania podsumowania użycia partnerów dla wszystkich klientów, którzy kupili określoną usługę lub zasób platformy Azure w bieżącym okresie rozliczeniowym.</span><span class="sxs-lookup"><span data-stu-id="bd396-108">You can use the **PartnerUsageSummary** resource to get a partner usage summary of all customers that purchased a specific Azure service or resource during the current billing period.</span></span>

<span data-ttu-id="bd396-109">*Łączna wartość zwrócona przez ten interfejs API nie zwróci zużycia dla klientów z planem platformy Azure.*</span><span class="sxs-lookup"><span data-stu-id="bd396-109">*The total returned by this API will not return consumption for customers that have an Azure plan.*</span></span> <span data-ttu-id="bd396-110">Planowane dla wycofania w przyszłości.</span><span class="sxs-lookup"><span data-stu-id="bd396-110">Planned for deprecation in the future.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="bd396-111">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="bd396-111">Prerequisites</span></span>

- <span data-ttu-id="bd396-112">Poświadczenia zgodnie z opisem w temacie [uwierzytelnianie w centrum partnerskim](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="bd396-112">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="bd396-113">Ten scenariusz obsługuje tylko uwierzytelnianie przy użyciu aplikacji i poświadczeń użytkownika.</span><span class="sxs-lookup"><span data-stu-id="bd396-113">This scenario supports authentication with App+User credentials only.</span></span>

## <a name="c"></a><span data-ttu-id="bd396-114">C\#</span><span class="sxs-lookup"><span data-stu-id="bd396-114">C\#</span></span>

<span data-ttu-id="bd396-115">Aby uzyskać podsumowanie użycia dla wszystkich klientów, którzy kupili określoną usługę lub zasób platformy Azure w bieżącym okresie rozliczeniowym:</span><span class="sxs-lookup"><span data-stu-id="bd396-115">To get a usage summary for all customers that purchased a specific Azure service or resource during the current billing period:</span></span>

1. <span data-ttu-id="bd396-116">Użyj **IAggregatePartner**.</span><span class="sxs-lookup"><span data-stu-id="bd396-116">Use your **IAggregatePartner**.</span></span>

2. <span data-ttu-id="bd396-117">Wywołaj Właściwość **UsageSummary** , a następnie metodę **Get ()** lub **GetAsync ()** :</span><span class="sxs-lookup"><span data-stu-id="bd396-117">Call the **UsageSummary** property, followed by the **Get()** or **GetAsync()** methods:</span></span>

    ``` csharp
    // IAggregatePartner partnerOperations;

    var usageSummary = partnerOperations.UsageSummary.Get();
    ```

<span data-ttu-id="bd396-118">Aby zapoznać się z przykładem, zobacz następujące tematy:</span><span class="sxs-lookup"><span data-stu-id="bd396-118">For an example, see the following:</span></span>

- <span data-ttu-id="bd396-119">Przykład: [aplikacja testowa konsoli](console-test-app.md)</span><span class="sxs-lookup"><span data-stu-id="bd396-119">Sample: [Console test app](console-test-app.md)</span></span>
- <span data-ttu-id="bd396-120">Projekt: **PartnerSDK. FeatureSamples**</span><span class="sxs-lookup"><span data-stu-id="bd396-120">Project: **PartnerSDK.FeatureSamples**</span></span>
- <span data-ttu-id="bd396-121">Klasa: **GetPartnerUsageSummary.cs**</span><span class="sxs-lookup"><span data-stu-id="bd396-121">Class: **GetPartnerUsageSummary.cs**</span></span>

## <a name="rest-request"></a><span data-ttu-id="bd396-122">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="bd396-122">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="bd396-123">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="bd396-123">Request syntax</span></span>

| <span data-ttu-id="bd396-124">Metoda</span><span class="sxs-lookup"><span data-stu-id="bd396-124">Method</span></span>  | <span data-ttu-id="bd396-125">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="bd396-125">Request URI</span></span>                                                         |
|---------|---------------------------------------------------------------------|
| <span data-ttu-id="bd396-126">**Pobierz**</span><span class="sxs-lookup"><span data-stu-id="bd396-126">**GET**</span></span> | <span data-ttu-id="bd396-127">[*{baseURL}*](partner-center-rest-urls.md)/V1/usagesummary http/1.1</span><span class="sxs-lookup"><span data-stu-id="bd396-127">[*{baseURL}*](partner-center-rest-urls.md)/v1/usagesummary HTTP/1.1</span></span> |

### <a name="request-headers"></a><span data-ttu-id="bd396-128">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="bd396-128">Request headers</span></span>

<span data-ttu-id="bd396-129">Aby uzyskać więcej informacji, zobacz [nagłówki REST Centrum partnerskiego](headers.md).</span><span class="sxs-lookup"><span data-stu-id="bd396-129">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="bd396-130">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="bd396-130">Request body</span></span>

<span data-ttu-id="bd396-131">Brak.</span><span class="sxs-lookup"><span data-stu-id="bd396-131">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="bd396-132">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="bd396-132">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/usagesummary HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: e128c8e2-4c33-4940-a3e2-2e59b0abdc67
MS-CorrelationId: 47c36033-af5d-4457-80a4-512c1626fac4
```

## <a name="rest-response"></a><span data-ttu-id="bd396-133">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="bd396-133">REST response</span></span>

<span data-ttu-id="bd396-134">Jeśli to się powiedzie, metoda zwraca zasób **PartnerUsageSummary** w treści odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="bd396-134">If successful, this method returns a **PartnerUsageSummary** resource in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="bd396-135">Kody sukcesu i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="bd396-135">Response success and error codes</span></span>

<span data-ttu-id="bd396-136">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie i dodatkowe informacje debugowania.</span><span class="sxs-lookup"><span data-stu-id="bd396-136">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="bd396-137">Użyj narzędzia do śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="bd396-137">Use a network trace tool to read this code, the error type, and additional parameters.</span></span> <span data-ttu-id="bd396-138">Aby uzyskać pełną listę, zobacz [kody błędów](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="bd396-138">For a full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="bd396-139">Przykład odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="bd396-139">Response example</span></span>

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
