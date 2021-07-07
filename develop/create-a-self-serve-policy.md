---
title: Tworzenie zasad samoobsługi
description: Jak utworzyć nowe zasady samoobsługi.
ms.date: 04/13/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 14f46e22fbd294c765b745204cf62474250cbfbd
ms.sourcegitcommit: ad8082bee01fb1f57da423b417ca1ca9c0df8e45
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/10/2021
ms.locfileid: "111973693"
---
# <a name="create-a-selfservepolicy"></a><span data-ttu-id="ab241-103">Tworzenie selfServePolicy</span><span class="sxs-lookup"><span data-stu-id="ab241-103">Create a SelfServePolicy</span></span>

<span data-ttu-id="ab241-104">W tym artykule wyjaśniono, jak utworzyć nowe zasady samoobsługi.</span><span class="sxs-lookup"><span data-stu-id="ab241-104">This article explains how to create a new self-serve policy.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ab241-105">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="ab241-105">Prerequisites</span></span>

- <span data-ttu-id="ab241-106">Poświadczenia zgodnie z opisem w te [Partner Center uwierzytelniania.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="ab241-106">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="ab241-107">Ten scenariusz obsługuje uwierzytelnianie przy użyciu poświadczeń aplikacji i użytkownika.</span><span class="sxs-lookup"><span data-stu-id="ab241-107">This scenario supports authentication with Application+User credentials.</span></span>

## <a name="c"></a><span data-ttu-id="ab241-108">C\#</span><span class="sxs-lookup"><span data-stu-id="ab241-108">C\#</span></span>

<span data-ttu-id="ab241-109">Utwórz zasady samoobsługowe:</span><span class="sxs-lookup"><span data-stu-id="ab241-109">Create a self-serve policy:</span></span>

1. <span data-ttu-id="ab241-110">Wywołaj [**metodę IAggregatePartner.SelfServePolicies.Create**](/dotnet/api/microsoft.store.partnercenter.iselfservepoliciescollection.create) lub [**IAggregatePartner.SelfServePolicies.CreateAsync**](/dotnet/api/microsoft.store.partnercenter.iselfservepoliciescollection.createasync) z informacjami o zasadach samoobsługi.</span><span class="sxs-lookup"><span data-stu-id="ab241-110">Call the [**IAggregatePartner.SelfServePolicies.Create**](/dotnet/api/microsoft.store.partnercenter.iselfservepoliciescollection.create) or [**IAggregatePartner.SelfServePolicies.CreateAsync**](/dotnet/api/microsoft.store.partnercenter.iselfservepoliciescollection.createasync) method with the self-serve policy info.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
string customerIdAsEntity;

var selfServePolicy = new SelfServePolicy
{
    SelfServeEntity = new SelfServeEntity
    {
        SelfServeEntityType = "customer",
        TenantID = customerIdAsEntity,
    },
    Grantor = new Grantor
    {
        GrantorType = "billToPartner",
        TenantID = partnerIdAsGrantor,
    },
    Permissions = new Permission[]
    {
        new Permission
        {
        Action = "Purchase",
        Resource = "AzureReservedInstances",
        },
    },
};

// All the operations executed on this partner operation instance will share the same correlation Id but will differ in request Id
IPartner scopedPartnerOperations = partnerOperations.With(RequestContextFactory.Instance.Create(Guid.NewGuid()));

// creates the self-serve policy
SelfServePolicy createdSelfServePolicy = scopedPartnerOperations.selfServePolicies.Create(selfServePolicy);
```

<span data-ttu-id="ab241-111">Przykład można znaleźć w następujących tematach:</span><span class="sxs-lookup"><span data-stu-id="ab241-111">For an example, see the following:</span></span>

- <span data-ttu-id="ab241-112">Przykład: [aplikacja testowa konsoli](console-test-app.md)</span><span class="sxs-lookup"><span data-stu-id="ab241-112">Sample: [Console test app](console-test-app.md)</span></span>
- <span data-ttu-id="ab241-113">Project: **PartnerSDK.FeatureSamples**</span><span class="sxs-lookup"><span data-stu-id="ab241-113">Project: **PartnerSDK.FeatureSamples**</span></span>
- <span data-ttu-id="ab241-114">Klasa: **CreateSelfServePolicies.cs**</span><span class="sxs-lookup"><span data-stu-id="ab241-114">Class: **CreateSelfServePolicies.cs**</span></span>


## <a name="rest-request"></a><span data-ttu-id="ab241-115">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="ab241-115">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="ab241-116">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="ab241-116">Request syntax</span></span>

| <span data-ttu-id="ab241-117">Metoda</span><span class="sxs-lookup"><span data-stu-id="ab241-117">Method</span></span>   | <span data-ttu-id="ab241-118">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="ab241-118">Request URI</span></span>                                                       |
|----------|-------------------------------------------------------------------|
| <span data-ttu-id="ab241-119">**Post**</span><span class="sxs-lookup"><span data-stu-id="ab241-119">**POST**</span></span> | <span data-ttu-id="ab241-120">[*{baseURL}*](partner-center-rest-urls.md)/v1/SelfServePolicy HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="ab241-120">[*{baseURL}*](partner-center-rest-urls.md)/v1/SelfServePolicy HTTP/1.1</span></span> |

### <a name="request-headers"></a><span data-ttu-id="ab241-121">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="ab241-121">Request headers</span></span>

- <span data-ttu-id="ab241-122">Wymagany jest identyfikator żądania i identyfikator korelacji.</span><span class="sxs-lookup"><span data-stu-id="ab241-122">A request ID and correlation ID are required.</span></span>
- <span data-ttu-id="ab241-123">Aby uzyskać więcej informacji, [zobacz Partner Center REST headers (Nagłówki REST).](headers.md)</span><span class="sxs-lookup"><span data-stu-id="ab241-123">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="ab241-124">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="ab241-124">Request body</span></span>

<span data-ttu-id="ab241-125">W tej tabeli opisano wymagane właściwości w treści żądania.</span><span class="sxs-lookup"><span data-stu-id="ab241-125">This table describes the required properties in the request body.</span></span>

| <span data-ttu-id="ab241-126">Nazwa</span><span class="sxs-lookup"><span data-stu-id="ab241-126">Name</span></span>                              | <span data-ttu-id="ab241-127">Typ</span><span class="sxs-lookup"><span data-stu-id="ab241-127">Type</span></span>   | <span data-ttu-id="ab241-128">Opis</span><span class="sxs-lookup"><span data-stu-id="ab241-128">Description</span></span>                                 |
|------------------------------------------------------------------|--------|---------------------------------------------|
| [<span data-ttu-id="ab241-129">SelfServePolicy</span><span class="sxs-lookup"><span data-stu-id="ab241-129">SelfServePolicy</span></span>](self-serve-policy-resources.md#selfservepolicy)| <span data-ttu-id="ab241-130">object</span><span class="sxs-lookup"><span data-stu-id="ab241-130">object</span></span> | <span data-ttu-id="ab241-131">Informacje o zasadach samoobsługi.</span><span class="sxs-lookup"><span data-stu-id="ab241-131">The self-serve policy information.</span></span> |

#### <a name="selfservepolicy"></a><span data-ttu-id="ab241-132">SelfServePolicy</span><span class="sxs-lookup"><span data-stu-id="ab241-132">SelfServePolicy</span></span>

<span data-ttu-id="ab241-133">W tej tabeli opisano minimalne wymagane pola z zasobu [SelfServePolicy](self-serve-policy-resources.md#selfservepolicy) potrzebne do utworzenia nowych zasad samoobsługi.</span><span class="sxs-lookup"><span data-stu-id="ab241-133">This table describes the minimum required fields from the [SelfServePolicy](self-serve-policy-resources.md#selfservepolicy) resource needed to create a new self-serve policy.</span></span>

| <span data-ttu-id="ab241-134">Właściwość</span><span class="sxs-lookup"><span data-stu-id="ab241-134">Property</span></span>              | <span data-ttu-id="ab241-135">Typ</span><span class="sxs-lookup"><span data-stu-id="ab241-135">Type</span></span>             | <span data-ttu-id="ab241-136">Opis</span><span class="sxs-lookup"><span data-stu-id="ab241-136">Description</span></span>                                                                                            |
|-----------------------|------------------|--------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="ab241-137">SelfServeEntity</span><span class="sxs-lookup"><span data-stu-id="ab241-137">SelfServeEntity</span></span>       | <span data-ttu-id="ab241-138">SelfServeEntity</span><span class="sxs-lookup"><span data-stu-id="ab241-138">SelfServeEntity</span></span>  | <span data-ttu-id="ab241-139">Jednostka samoobsługi, która ma przyznany dostęp.</span><span class="sxs-lookup"><span data-stu-id="ab241-139">The self-serve entity that is being granted access.</span></span>                                                     |
| <span data-ttu-id="ab241-140">Grantor</span><span class="sxs-lookup"><span data-stu-id="ab241-140">Grantor</span></span>               | <span data-ttu-id="ab241-141">Grantor</span><span class="sxs-lookup"><span data-stu-id="ab241-141">Grantor</span></span>          | <span data-ttu-id="ab241-142">Grantor, który udziela dostępu.</span><span class="sxs-lookup"><span data-stu-id="ab241-142">The grantor that is granting access.</span></span>                                                                    |
| <span data-ttu-id="ab241-143">Uprawnienia</span><span class="sxs-lookup"><span data-stu-id="ab241-143">Permissions</span></span>           | <span data-ttu-id="ab241-144">Tablica uprawnień</span><span class="sxs-lookup"><span data-stu-id="ab241-144">Array of Permission</span></span>| <span data-ttu-id="ab241-145">Tablica [zasobów](self-serve-policy-resources.md#permission) uprawnień.</span><span class="sxs-lookup"><span data-stu-id="ab241-145">An Array of [Permission](self-serve-policy-resources.md#permission) resources.</span></span>                                                                     |


### <a name="request-example"></a><span data-ttu-id="ab241-146">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="ab241-146">Request example</span></span>

```http
POST https://api.partnercenter.microsoft.com/v1/SelfServePolicy HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 94e4e214-6b06-4fb7-96d1-94d559f9b47f
MS-CorrelationId: ab993325-1605-4cf4-bac4-fb584142a31b
X-Locale: en-US
Content-Type: application/json
Host: api.partnercenter.microsoft.com
Content-Length: 789
Expect: 100-continue
Connection: Keep-Alive

{
    "selfServeEntity": {
        "selfServeEntityType": "customer",
        "tenantID": "0431a72c-7d8a-4393-b25e-ef63f5efb415"
    },
    "grantor": {
        "grantorType": "billToPartner",
        "tenantID": "634f6379-ad54-449b-9821-564f737158ab"
    },
    "permissions": [{
        "resource": "AzureReservedInstances",
        "action": "Purchase"
    }
}
```

## <a name="rest-response"></a><span data-ttu-id="ab241-147">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="ab241-147">REST response</span></span>

<span data-ttu-id="ab241-148">Jeśli to się powiedzie, ten interfejs API zwraca [zasób SelfServePolicy](self-serve-policy-resources.md#selfservepolicy) dla nowych zasad samoobsługi.</span><span class="sxs-lookup"><span data-stu-id="ab241-148">If successful, this API returns a [SelfServePolicy](self-serve-policy-resources.md#selfservepolicy) resource for the new self-serve policy.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="ab241-149">Kody powodzenia i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="ab241-149">Response success and error codes</span></span>

<span data-ttu-id="ab241-150">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie, oraz dodatkowe informacje o debugowaniu.</span><span class="sxs-lookup"><span data-stu-id="ab241-150">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="ab241-151">Użyj narzędzia śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="ab241-151">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="ab241-152">Aby uzyskać pełną listę, zobacz [Partner Center kodów błędów REST.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="ab241-152">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

<span data-ttu-id="ab241-153">Ta metoda zwraca następujące kody błędów:</span><span class="sxs-lookup"><span data-stu-id="ab241-153">This method returns the following error codes:</span></span>

| <span data-ttu-id="ab241-154">Kod stanu HTTP</span><span class="sxs-lookup"><span data-stu-id="ab241-154">HTTP Status Code</span></span>     | <span data-ttu-id="ab241-155">Kod błędu</span><span class="sxs-lookup"><span data-stu-id="ab241-155">Error code</span></span>   | <span data-ttu-id="ab241-156">Opis</span><span class="sxs-lookup"><span data-stu-id="ab241-156">Description</span></span>                                                                |
|----------------------|--------------|----------------------------------------------------------------------------|
| <span data-ttu-id="ab241-157">409</span><span class="sxs-lookup"><span data-stu-id="ab241-157">409</span></span>                  | <span data-ttu-id="ab241-158">600041</span><span class="sxs-lookup"><span data-stu-id="ab241-158">600041</span></span>       | <span data-ttu-id="ab241-159">Zasady samoobsługi już istnieją.</span><span class="sxs-lookup"><span data-stu-id="ab241-159">Self-serve policy already exists.</span></span>                                                     |


### <a name="response-example"></a><span data-ttu-id="ab241-160">Przykład odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="ab241-160">Response example</span></span>

```http
HTTP/1.1 201 Created
Content-Length: 834
Content-Type: application/json; charset=utf-8
MS-CorrelationId: ab993325-1605-4cf4-bac4-fb584142a31b
MS-RequestId: 94e4e214-6b06-4fb7-96d1-94d559f9b47f
Date: Tue, 14 Feb 2017 20:06:02 GMT

{
    "id": "634f6379-ad54-449b-9821-564f737158ab_0431a72c-7d8a-4393-b25e-ef63f5efb415",
    "selfServeEntity": {
        "selfServeEntityType": "customer",
        "tenantID": "0431a72c-7d8a-4393-b25e-ef63f5efb415"
    },
    "grantor": {
        "grantorType": "billToPartner",
        "tenantID": "634f6379-ad54-449b-9821-564f737158ab"
    },
    "permissions": [{
        "resource": "AzureReservedInstances",
        "action": "Purchase"
    }],
    "attributes": {
        "etag": "\"933523d1-3f63-4fc3-8789-5e21c02cdaed\"",
        "objectType": "SelfServePolicy"
    }
}
```
