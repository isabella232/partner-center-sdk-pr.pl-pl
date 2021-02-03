---
title: Tworzenie zasad samoobsługi
description: Jak utworzyć nowe zasady samoobsługi.
ms.date: 04/13/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: fd1579b2775ead57a440db0d6afb3bf22164c319
ms.sourcegitcommit: 01e75175077611da92175c777a440a594fb05797
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/08/2020
ms.locfileid: "97770219"
---
# <a name="create-a-selfservepolicy"></a><span data-ttu-id="9695d-103">Utwórz SelfServePolicy</span><span class="sxs-lookup"><span data-stu-id="9695d-103">Create a SelfServePolicy</span></span>

<span data-ttu-id="9695d-104">**Dotyczy:**</span><span class="sxs-lookup"><span data-stu-id="9695d-104">**Applies to:**</span></span>

- <span data-ttu-id="9695d-105">Centrum partnerskie</span><span class="sxs-lookup"><span data-stu-id="9695d-105">Partner Center</span></span>

<span data-ttu-id="9695d-106">W tym temacie opisano sposób tworzenia nowych zasad samoobsługi.</span><span class="sxs-lookup"><span data-stu-id="9695d-106">This topic explains how to create a new self-serve policy.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9695d-107">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="9695d-107">Prerequisites</span></span>

- <span data-ttu-id="9695d-108">Poświadczenia zgodnie z opisem w temacie [uwierzytelnianie w centrum partnerskim](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="9695d-108">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="9695d-109">Ten scenariusz obsługuje uwierzytelnianie przy użyciu poświadczeń aplikacji i użytkownika.</span><span class="sxs-lookup"><span data-stu-id="9695d-109">This scenario supports authentication with Application+User credentials.</span></span>

## <a name="c"></a><span data-ttu-id="9695d-110">C\#</span><span class="sxs-lookup"><span data-stu-id="9695d-110">C\#</span></span>

<span data-ttu-id="9695d-111">Utwórz zasady samoobsługi:</span><span class="sxs-lookup"><span data-stu-id="9695d-111">Create a self-serve policy:</span></span>

1. <span data-ttu-id="9695d-112">Wywołaj metodę [**IAggregatePartner. SelfServePolicies. Create**](/dotnet/api/microsoft.store.partnercenter.iselfservepoliciescollection.create) lub [**IAggregatePartner. SelfServePolicies. onasync**](/dotnet/api/microsoft.store.partnercenter.iselfservepoliciescollection.createasync) z informacjami o zasadach samoobsługi.</span><span class="sxs-lookup"><span data-stu-id="9695d-112">Call the [**IAggregatePartner.SelfServePolicies.Create**](/dotnet/api/microsoft.store.partnercenter.iselfservepoliciescollection.create) or [**IAggregatePartner.SelfServePolicies.CreateAsync**](/dotnet/api/microsoft.store.partnercenter.iselfservepoliciescollection.createasync) method with the self-serve policy info.</span></span>

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

<span data-ttu-id="9695d-113">Aby zapoznać się z przykładem, zobacz następujące tematy:</span><span class="sxs-lookup"><span data-stu-id="9695d-113">For an example, see the following:</span></span>

- <span data-ttu-id="9695d-114">Przykład: [aplikacja testowa konsoli](console-test-app.md)</span><span class="sxs-lookup"><span data-stu-id="9695d-114">Sample: [Console test app](console-test-app.md)</span></span>
- <span data-ttu-id="9695d-115">Projekt: **PartnerSDK. FeatureSamples**</span><span class="sxs-lookup"><span data-stu-id="9695d-115">Project: **PartnerSDK.FeatureSamples**</span></span>
- <span data-ttu-id="9695d-116">Klasa: **CreateSelfServePolicies.cs**</span><span class="sxs-lookup"><span data-stu-id="9695d-116">Class: **CreateSelfServePolicies.cs**</span></span>


## <a name="rest-request"></a><span data-ttu-id="9695d-117">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="9695d-117">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="9695d-118">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="9695d-118">Request syntax</span></span>

| <span data-ttu-id="9695d-119">Metoda</span><span class="sxs-lookup"><span data-stu-id="9695d-119">Method</span></span>   | <span data-ttu-id="9695d-120">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="9695d-120">Request URI</span></span>                                                       |
|----------|-------------------------------------------------------------------|
| <span data-ttu-id="9695d-121">**POUBOJOWEGO**</span><span class="sxs-lookup"><span data-stu-id="9695d-121">**POST**</span></span> | <span data-ttu-id="9695d-122">[*{baseURL}*](partner-center-rest-urls.md)/V1/SelfServePolicy http/1.1</span><span class="sxs-lookup"><span data-stu-id="9695d-122">[*{baseURL}*](partner-center-rest-urls.md)/v1/SelfServePolicy HTTP/1.1</span></span> |

### <a name="request-headers"></a><span data-ttu-id="9695d-123">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="9695d-123">Request headers</span></span>

- <span data-ttu-id="9695d-124">Identyfikator żądania i identyfikator korelacji są wymagane.</span><span class="sxs-lookup"><span data-stu-id="9695d-124">A request ID and correlation ID are required.</span></span>
- <span data-ttu-id="9695d-125">Aby uzyskać więcej informacji, zobacz [nagłówki REST Centrum partnerskiego](headers.md) .</span><span class="sxs-lookup"><span data-stu-id="9695d-125">See [Partner Center REST headers](headers.md) for more information.</span></span>

### <a name="request-body"></a><span data-ttu-id="9695d-126">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="9695d-126">Request body</span></span>

<span data-ttu-id="9695d-127">W tej tabeli opisano wymagane właściwości w treści żądania.</span><span class="sxs-lookup"><span data-stu-id="9695d-127">This table describes the required properties in the request body.</span></span>

| <span data-ttu-id="9695d-128">Nazwa</span><span class="sxs-lookup"><span data-stu-id="9695d-128">Name</span></span>                              | <span data-ttu-id="9695d-129">Typ</span><span class="sxs-lookup"><span data-stu-id="9695d-129">Type</span></span>   | <span data-ttu-id="9695d-130">Opis</span><span class="sxs-lookup"><span data-stu-id="9695d-130">Description</span></span>                                 |
|------------------------------------------------------------------|--------|---------------------------------------------|
| [<span data-ttu-id="9695d-131">SelfServePolicy</span><span class="sxs-lookup"><span data-stu-id="9695d-131">SelfServePolicy</span></span>](self-serve-policy-resources.md#selfservepolicy)| <span data-ttu-id="9695d-132">object</span><span class="sxs-lookup"><span data-stu-id="9695d-132">object</span></span> | <span data-ttu-id="9695d-133">Informacje o zasadach samoobsługi.</span><span class="sxs-lookup"><span data-stu-id="9695d-133">The self-serve policy information.</span></span> |

#### <a name="selfservepolicy"></a><span data-ttu-id="9695d-134">SelfServePolicy</span><span class="sxs-lookup"><span data-stu-id="9695d-134">SelfServePolicy</span></span>

<span data-ttu-id="9695d-135">Ta tabela zawiera opis minimalnych wymaganych pól z zasobów [SelfServePolicy](self-serve-policy-resources.md#selfservepolicy) wymaganych do utworzenia nowych zasad samoobsługi.</span><span class="sxs-lookup"><span data-stu-id="9695d-135">This table describes the minimum required fields from the [SelfServePolicy](self-serve-policy-resources.md#selfservepolicy) resource needed to create a new self-serve policy.</span></span>

| <span data-ttu-id="9695d-136">Właściwość</span><span class="sxs-lookup"><span data-stu-id="9695d-136">Property</span></span>              | <span data-ttu-id="9695d-137">Typ</span><span class="sxs-lookup"><span data-stu-id="9695d-137">Type</span></span>             | <span data-ttu-id="9695d-138">Opis</span><span class="sxs-lookup"><span data-stu-id="9695d-138">Description</span></span>                                                                                            |
|-----------------------|------------------|--------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="9695d-139">SelfServeEntity</span><span class="sxs-lookup"><span data-stu-id="9695d-139">SelfServeEntity</span></span>       | <span data-ttu-id="9695d-140">SelfServeEntity</span><span class="sxs-lookup"><span data-stu-id="9695d-140">SelfServeEntity</span></span>  | <span data-ttu-id="9695d-141">Samoobsługowa jednostka, do której uzyskuje się dostęp.</span><span class="sxs-lookup"><span data-stu-id="9695d-141">The self-serve entity that is being granted access.</span></span>                                                     |
| <span data-ttu-id="9695d-142">Użytkownik udzielający uprawnienia</span><span class="sxs-lookup"><span data-stu-id="9695d-142">Grantor</span></span>               | <span data-ttu-id="9695d-143">Użytkownik udzielający uprawnienia</span><span class="sxs-lookup"><span data-stu-id="9695d-143">Grantor</span></span>          | <span data-ttu-id="9695d-144">Użytkownik udzielający uprawnienia udzielający dostępu.</span><span class="sxs-lookup"><span data-stu-id="9695d-144">The grantor that is granting access.</span></span>                                                                    |
| <span data-ttu-id="9695d-145">Uprawnienia</span><span class="sxs-lookup"><span data-stu-id="9695d-145">Permissions</span></span>           | <span data-ttu-id="9695d-146">Tablica uprawnień</span><span class="sxs-lookup"><span data-stu-id="9695d-146">Array of Permission</span></span>| <span data-ttu-id="9695d-147">Tablica zasobów [uprawnień](self-serve-policy-resources.md#permission) .</span><span class="sxs-lookup"><span data-stu-id="9695d-147">An Array of [Permission](self-serve-policy-resources.md#permission) resources.</span></span>                                                                     |


### <a name="request-example"></a><span data-ttu-id="9695d-148">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="9695d-148">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="9695d-149">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="9695d-149">REST response</span></span>

<span data-ttu-id="9695d-150">Jeśli to się powiedzie, ten interfejs API zwraca zasób [SelfServePolicy](self-serve-policy-resources.md#selfservepolicy) dla nowych zasad samoobsługi.</span><span class="sxs-lookup"><span data-stu-id="9695d-150">If successful, this API returns a [SelfServePolicy](self-serve-policy-resources.md#selfservepolicy) resource for the new self-serve policy.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="9695d-151">Kody sukcesu i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="9695d-151">Response success and error codes</span></span>

<span data-ttu-id="9695d-152">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie i dodatkowe informacje debugowania.</span><span class="sxs-lookup"><span data-stu-id="9695d-152">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="9695d-153">Użyj narzędzia do śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="9695d-153">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="9695d-154">Aby uzyskać pełną listę, zobacz [kody błędów REST centrum partnera](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="9695d-154">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

<span data-ttu-id="9695d-155">Ta metoda zwraca następujące kody błędów:</span><span class="sxs-lookup"><span data-stu-id="9695d-155">This method returns the following error codes:</span></span>

| <span data-ttu-id="9695d-156">Kod stanu HTTP</span><span class="sxs-lookup"><span data-stu-id="9695d-156">HTTP Status Code</span></span>     | <span data-ttu-id="9695d-157">Kod błędu</span><span class="sxs-lookup"><span data-stu-id="9695d-157">Error code</span></span>   | <span data-ttu-id="9695d-158">Opis</span><span class="sxs-lookup"><span data-stu-id="9695d-158">Description</span></span>                                                                |
|----------------------|--------------|----------------------------------------------------------------------------|
| <span data-ttu-id="9695d-159">409</span><span class="sxs-lookup"><span data-stu-id="9695d-159">409</span></span>                  | <span data-ttu-id="9695d-160">600041</span><span class="sxs-lookup"><span data-stu-id="9695d-160">600041</span></span>       | <span data-ttu-id="9695d-161">Zasady samoobsługowe już istnieją.</span><span class="sxs-lookup"><span data-stu-id="9695d-161">Self-serve policy already exists.</span></span>                                                     |


### <a name="response-example"></a><span data-ttu-id="9695d-162">Przykład odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="9695d-162">Response example</span></span>

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
