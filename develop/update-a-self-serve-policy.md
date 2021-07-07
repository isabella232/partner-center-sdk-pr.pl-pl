---
title: Aktualizowanie zasad samoobsługi
description: Jak zaktualizować zasady samoobsługi.
ms.date: 04/13/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: d94382e73fd2a79751fe5f8f8414df2befde584f
ms.sourcegitcommit: 0b2a62af1765a447addd9c4340c28bc42fdc2747
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/04/2021
ms.locfileid: "111445259"
---
# <a name="update-a-selfservepolicy"></a><span data-ttu-id="e21dc-103">Aktualizowanie selfServePolicy</span><span class="sxs-lookup"><span data-stu-id="e21dc-103">Update a SelfServePolicy</span></span>

<span data-ttu-id="e21dc-104">W tym artykule wyjaśniono, jak zaktualizować zasady samoobsługi.</span><span class="sxs-lookup"><span data-stu-id="e21dc-104">This article explains how to update a self-serve policy.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e21dc-105">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="e21dc-105">Prerequisites</span></span>

- <span data-ttu-id="e21dc-106">Poświadczenia zgodnie z opisem w te [Partner Center uwierzytelniania.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="e21dc-106">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="e21dc-107">Ten scenariusz obsługuje uwierzytelnianie przy użyciu poświadczeń aplikacji i użytkownika.</span><span class="sxs-lookup"><span data-stu-id="e21dc-107">This scenario supports authentication with Application+User credentials.</span></span>

## <a name="c"></a><span data-ttu-id="e21dc-108">C\#</span><span class="sxs-lookup"><span data-stu-id="e21dc-108">C\#</span></span>

<span data-ttu-id="e21dc-109">Aby usunąć zasady samoobsługi:</span><span class="sxs-lookup"><span data-stu-id="e21dc-109">To delete a self-serve policy:</span></span>

1. <span data-ttu-id="e21dc-110">Wywołaj [**metodę IAggregatePartner.SelfServePolicies.ById**](/dotnet/api/microsoft.store.partnercenter.iselfservepoliciescollection.byid) z identyfikatorem jednostki, aby pobrać interfejs do operacji na zasadach.</span><span class="sxs-lookup"><span data-stu-id="e21dc-110">Call the [**IAggregatePartner.SelfServePolicies.ById**](/dotnet/api/microsoft.store.partnercenter.iselfservepoliciescollection.byid) method with the entity identifier to retrieve an interface to operations on the policies.</span></span>

2. <span data-ttu-id="e21dc-111">Wywołaj [**metodę Put**](/dotnet/api/microsoft.store.partnercenter.SelfServePolicies.put) lub [**PutAsync,**](/dotnet/api/microsoft.store.partnercenter.SelfServePolicies.putasync) aby zaktualizować zasady samoobsługi.</span><span class="sxs-lookup"><span data-stu-id="e21dc-111">Call the [**Put**](/dotnet/api/microsoft.store.partnercenter.SelfServePolicies.put) or [**PutAsync**](/dotnet/api/microsoft.store.partnercenter.SelfServePolicies.putasync) method to update the self-serve policy.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
SelfServePolicy policy;

// All the operations executed on this partner operation instance will share the same correlation identifier but will differ in request identifier
IPartner scopedPartnerOperations = partnerOperations.With(RequestContextFactory.Instance.Create(Guid.NewGuid()));

// updates the self-serve policies
partnerOperations.SelfServePolicies.ById(policy.id).Put(policy);
```

## <a name="rest-request"></a><span data-ttu-id="e21dc-112">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="e21dc-112">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="e21dc-113">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="e21dc-113">Request syntax</span></span>

| <span data-ttu-id="e21dc-114">Metoda</span><span class="sxs-lookup"><span data-stu-id="e21dc-114">Method</span></span>   | <span data-ttu-id="e21dc-115">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="e21dc-115">Request URI</span></span>                                                       |
|----------|-------------------------------------------------------------------|
| <span data-ttu-id="e21dc-116">**PUT**</span><span class="sxs-lookup"><span data-stu-id="e21dc-116">**PUT**</span></span> | <span data-ttu-id="e21dc-117">[*{baseURL}*](partner-center-rest-urls.md)/v1/SelfServePolicy HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="e21dc-117">[*{baseURL}*](partner-center-rest-urls.md)/v1/SelfServePolicy HTTP/1.1</span></span> |

### <a name="request-headers"></a><span data-ttu-id="e21dc-118">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="e21dc-118">Request headers</span></span>

- <span data-ttu-id="e21dc-119">Wymagany jest identyfikator żądania i identyfikator korelacji.</span><span class="sxs-lookup"><span data-stu-id="e21dc-119">A request identifier and correlation identifier are required.</span></span>
- <span data-ttu-id="e21dc-120">Aby uzyskać więcej informacji, [zobacz Partner Center REST headers (Nagłówki REST).](headers.md)</span><span class="sxs-lookup"><span data-stu-id="e21dc-120">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="e21dc-121">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="e21dc-121">Request body</span></span>

<span data-ttu-id="e21dc-122">W tej tabeli opisano wymagane właściwości w treści żądania.</span><span class="sxs-lookup"><span data-stu-id="e21dc-122">This table describes the required properties in the request body.</span></span>

| <span data-ttu-id="e21dc-123">Nazwa</span><span class="sxs-lookup"><span data-stu-id="e21dc-123">Name</span></span>                              | <span data-ttu-id="e21dc-124">Typ</span><span class="sxs-lookup"><span data-stu-id="e21dc-124">Type</span></span>   | <span data-ttu-id="e21dc-125">Opis</span><span class="sxs-lookup"><span data-stu-id="e21dc-125">Description</span></span>                                 |
|------------------------------------------------------------------|--------|---------------------------------------------|
| [<span data-ttu-id="e21dc-126">SelfServePolicy</span><span class="sxs-lookup"><span data-stu-id="e21dc-126">SelfServePolicy</span></span>](self-serve-policy-resources.md#selfservepolicy)| <span data-ttu-id="e21dc-127">object</span><span class="sxs-lookup"><span data-stu-id="e21dc-127">object</span></span> | <span data-ttu-id="e21dc-128">Informacje o zasadach samoobsługi.</span><span class="sxs-lookup"><span data-stu-id="e21dc-128">The self-serve policy information.</span></span> |

#### <a name="selfservepolicy"></a><span data-ttu-id="e21dc-129">SelfServePolicy</span><span class="sxs-lookup"><span data-stu-id="e21dc-129">SelfServePolicy</span></span>

<span data-ttu-id="e21dc-130">W tej tabeli opisano minimalne wymagane pola z zasobu [SelfServePolicy](self-serve-policy-resources.md#selfservepolicy) potrzebne do utworzenia nowych zasad samoobsługi.</span><span class="sxs-lookup"><span data-stu-id="e21dc-130">This table describes the minimum required fields from the [SelfServePolicy](self-serve-policy-resources.md#selfservepolicy) resource needed to create a new self-serve policy.</span></span>

| <span data-ttu-id="e21dc-131">Właściwość</span><span class="sxs-lookup"><span data-stu-id="e21dc-131">Property</span></span>              | <span data-ttu-id="e21dc-132">Typ</span><span class="sxs-lookup"><span data-stu-id="e21dc-132">Type</span></span>             | <span data-ttu-id="e21dc-133">Opis</span><span class="sxs-lookup"><span data-stu-id="e21dc-133">Description</span></span>                                                                                            |
|-----------------------|------------------|--------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="e21dc-134">identyfikator</span><span class="sxs-lookup"><span data-stu-id="e21dc-134">id</span></span>                    | <span data-ttu-id="e21dc-135">ciąg</span><span class="sxs-lookup"><span data-stu-id="e21dc-135">string</span></span>           | <span data-ttu-id="e21dc-136">Identyfikator zasad samoobsługi, który jest dostarczany po pomyślnym utworzeniu zasad samoobsługi.</span><span class="sxs-lookup"><span data-stu-id="e21dc-136">A self-serve policy identifier that is supplied upon successful creation of the self-serve policy.</span></span>     |
| <span data-ttu-id="e21dc-137">SelfServeEntity</span><span class="sxs-lookup"><span data-stu-id="e21dc-137">SelfServeEntity</span></span>       | <span data-ttu-id="e21dc-138">SelfServeEntity</span><span class="sxs-lookup"><span data-stu-id="e21dc-138">SelfServeEntity</span></span>  | <span data-ttu-id="e21dc-139">Jednostka samoobsługi, która ma przyznany dostęp.</span><span class="sxs-lookup"><span data-stu-id="e21dc-139">The self-serve entity that is being granted access.</span></span>                                                     |
| <span data-ttu-id="e21dc-140">Grantor</span><span class="sxs-lookup"><span data-stu-id="e21dc-140">Grantor</span></span>               | <span data-ttu-id="e21dc-141">Grantor</span><span class="sxs-lookup"><span data-stu-id="e21dc-141">Grantor</span></span>          | <span data-ttu-id="e21dc-142">Grantor, który udziela dostępu.</span><span class="sxs-lookup"><span data-stu-id="e21dc-142">The grantor that is granting access.</span></span>                                                                    |
| <span data-ttu-id="e21dc-143">Uprawnienia</span><span class="sxs-lookup"><span data-stu-id="e21dc-143">Permissions</span></span>           | <span data-ttu-id="e21dc-144">Tablica uprawnień</span><span class="sxs-lookup"><span data-stu-id="e21dc-144">Array of Permission</span></span>| <span data-ttu-id="e21dc-145">Tablica [zasobów](self-serve-policy-resources.md#permission) uprawnień.</span><span class="sxs-lookup"><span data-stu-id="e21dc-145">An Array of [Permission](self-serve-policy-resources.md#permission) resources.</span></span>                                                      |
| <span data-ttu-id="e21dc-146">Etag</span><span class="sxs-lookup"><span data-stu-id="e21dc-146">Etag</span></span>                  | <span data-ttu-id="e21dc-147">ciąg</span><span class="sxs-lookup"><span data-stu-id="e21dc-147">string</span></span>           | <span data-ttu-id="e21dc-148">Tag Etag.</span><span class="sxs-lookup"><span data-stu-id="e21dc-148">The Etag.</span></span>                                                                                               |


### <a name="request-example"></a><span data-ttu-id="e21dc-149">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="e21dc-149">Request example</span></span>

```http
PUT https://api.partnercenter.microsoft.com/v1/SelfServePolicy HTTP/1.1
Authorization: Bearer <token>
MS-RequestId: 94e4e214-6b06-4fb7-96d1-94d559f9b47f
MS-CorrelationId: ab993325-1605-4cf4-bac4-fb584142a31b
Content-Type: application/json
Host: api.partnercenter.microsoft.com
Connection: Keep-Alive

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

## <a name="rest-response"></a><span data-ttu-id="e21dc-150">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="e21dc-150">REST response</span></span>

<span data-ttu-id="e21dc-151">Jeśli to się powiedzie, ten interfejs API zwraca [zasób SelfServePolicy](self-serve-policy-resources.md#selfservepolicy) dla zaktualizowanych zasad samoobsługi.</span><span class="sxs-lookup"><span data-stu-id="e21dc-151">If successful, this API returns a [SelfServePolicy](self-serve-policy-resources.md#selfservepolicy) resource for the updated self-serve policy.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="e21dc-152">Kody powodzenia i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="e21dc-152">Response success and error codes</span></span>

<span data-ttu-id="e21dc-153">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie, oraz dodatkowe informacje o debugowaniu.</span><span class="sxs-lookup"><span data-stu-id="e21dc-153">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="e21dc-154">Użyj narzędzia śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="e21dc-154">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="e21dc-155">Aby uzyskać pełną listę, zobacz [Partner Center kodów błędów REST.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="e21dc-155">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

<span data-ttu-id="e21dc-156">Ta metoda zwraca następujące kody błędów:</span><span class="sxs-lookup"><span data-stu-id="e21dc-156">This method returns the following error codes:</span></span>

| <span data-ttu-id="e21dc-157">Kod stanu HTTP</span><span class="sxs-lookup"><span data-stu-id="e21dc-157">HTTP Status Code</span></span>     | <span data-ttu-id="e21dc-158">Kod błędu</span><span class="sxs-lookup"><span data-stu-id="e21dc-158">Error code</span></span>   | <span data-ttu-id="e21dc-159">Opis</span><span class="sxs-lookup"><span data-stu-id="e21dc-159">Description</span></span>                                                                |
|----------------------|--------------|----------------------------------------------------------------------------|
| <span data-ttu-id="e21dc-160">404</span><span class="sxs-lookup"><span data-stu-id="e21dc-160">404</span></span>                  | <span data-ttu-id="e21dc-161">600039</span><span class="sxs-lookup"><span data-stu-id="e21dc-161">600039</span></span>       | <span data-ttu-id="e21dc-162">Nie znaleziono zasad samoobsługi</span><span class="sxs-lookup"><span data-stu-id="e21dc-162">Self-serve policy was not found</span></span>                                            |
| <span data-ttu-id="e21dc-163">404</span><span class="sxs-lookup"><span data-stu-id="e21dc-163">404</span></span>                  | <span data-ttu-id="e21dc-164">600040</span><span class="sxs-lookup"><span data-stu-id="e21dc-164">600040</span></span>       | <span data-ttu-id="e21dc-165">Identyfikator zasad samoobsługi jest nieprawidłowy</span><span class="sxs-lookup"><span data-stu-id="e21dc-165">Self-serve policy identifier is incorrect</span></span>                                  |


### <a name="response-example"></a><span data-ttu-id="e21dc-166">Przykład odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="e21dc-166">Response example</span></span>

```http
HTTP/1.1 200 Ok
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
        "etag": "\"1ec98034-a249-46f4-b9dd-9cd464fb5e47\"",
        "objectType": "SelfServePolicy"
    }
}
```
