---
title: Aktualizowanie zasad samoobsługi
description: Jak zaktualizować zasady samoobsługowe.
ms.date: 04/13/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 4d53ab8e5b8ef5b7be83360a3f43ec7791b2e3b4
ms.sourcegitcommit: 01e75175077611da92175c777a440a594fb05797
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/08/2020
ms.locfileid: "97770251"
---
# <a name="update-a-selfservepolicy"></a><span data-ttu-id="06695-103">Aktualizowanie elementu SelfServePolicy</span><span class="sxs-lookup"><span data-stu-id="06695-103">Update a SelfServePolicy</span></span>

<span data-ttu-id="06695-104">**Dotyczy:**</span><span class="sxs-lookup"><span data-stu-id="06695-104">**Applies to:**</span></span>

- <span data-ttu-id="06695-105">Centrum partnerskie</span><span class="sxs-lookup"><span data-stu-id="06695-105">Partner Center</span></span>

<span data-ttu-id="06695-106">W tym temacie opisano sposób aktualizowania zasad samoobsługi.</span><span class="sxs-lookup"><span data-stu-id="06695-106">This topic explains how to update a self-serve policy.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="06695-107">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="06695-107">Prerequisites</span></span>

- <span data-ttu-id="06695-108">Poświadczenia zgodnie z opisem w temacie [uwierzytelnianie w centrum partnerskim](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="06695-108">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="06695-109">Ten scenariusz obsługuje uwierzytelnianie przy użyciu poświadczeń aplikacji i użytkownika.</span><span class="sxs-lookup"><span data-stu-id="06695-109">This scenario supports authentication with Application+User credentials.</span></span>

## <a name="c"></a><span data-ttu-id="06695-110">C\#</span><span class="sxs-lookup"><span data-stu-id="06695-110">C\#</span></span>

<span data-ttu-id="06695-111">Aby usunąć zasady samoobsługowe:</span><span class="sxs-lookup"><span data-stu-id="06695-111">To delete a self-serve policy:</span></span>

1. <span data-ttu-id="06695-112">Wywołaj metodę [**IAggregatePartner. SelfServePolicies. ById**](/dotnet/api/microsoft.store.partnercenter.iselfservepoliciescollection.byid) z identyfikatorem jednostki, aby pobrać interfejs do operacji w ramach zasad.</span><span class="sxs-lookup"><span data-stu-id="06695-112">Call the [**IAggregatePartner.SelfServePolicies.ById**](/dotnet/api/microsoft.store.partnercenter.iselfservepoliciescollection.byid) method with the entity identifier to retrieve an interface to operations on the policies.</span></span>

2. <span data-ttu-id="06695-113">Wywołaj metodę [**Put**](/dotnet/api/microsoft.store.partnercenter.SelfServePolicies.put) lub [**PutAsync**](/dotnet/api/microsoft.store.partnercenter.SelfServePolicies.putasync) w celu zaktualizowania zasad samoobsługi.</span><span class="sxs-lookup"><span data-stu-id="06695-113">Call the [**Put**](/dotnet/api/microsoft.store.partnercenter.SelfServePolicies.put) or [**PutAsync**](/dotnet/api/microsoft.store.partnercenter.SelfServePolicies.putasync) method to update the self-serve policy.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
SelfServePolicy policy;

// All the operations executed on this partner operation instance will share the same correlation identifier but will differ in request identifier
IPartner scopedPartnerOperations = partnerOperations.With(RequestContextFactory.Instance.Create(Guid.NewGuid()));

// updates the self-serve policies
partnerOperations.SelfServePolicies.ById(policy.id).Put(policy);
```

## <a name="rest-request"></a><span data-ttu-id="06695-114">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="06695-114">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="06695-115">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="06695-115">Request syntax</span></span>

| <span data-ttu-id="06695-116">Metoda</span><span class="sxs-lookup"><span data-stu-id="06695-116">Method</span></span>   | <span data-ttu-id="06695-117">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="06695-117">Request URI</span></span>                                                       |
|----------|-------------------------------------------------------------------|
| <span data-ttu-id="06695-118">**PUT**</span><span class="sxs-lookup"><span data-stu-id="06695-118">**PUT**</span></span> | <span data-ttu-id="06695-119">[*{baseURL}*](partner-center-rest-urls.md)/V1/SelfServePolicy http/1.1</span><span class="sxs-lookup"><span data-stu-id="06695-119">[*{baseURL}*](partner-center-rest-urls.md)/v1/SelfServePolicy HTTP/1.1</span></span> |

### <a name="request-headers"></a><span data-ttu-id="06695-120">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="06695-120">Request headers</span></span>

- <span data-ttu-id="06695-121">Wymagany jest identyfikator żądania i identyfikator korelacji.</span><span class="sxs-lookup"><span data-stu-id="06695-121">A request identifier and correlation identifier are required.</span></span>
- <span data-ttu-id="06695-122">Aby uzyskać więcej informacji, zobacz [nagłówki REST Centrum partnerskiego](headers.md) .</span><span class="sxs-lookup"><span data-stu-id="06695-122">See [Partner Center REST headers](headers.md) for more information.</span></span>

### <a name="request-body"></a><span data-ttu-id="06695-123">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="06695-123">Request body</span></span>

<span data-ttu-id="06695-124">W tej tabeli opisano wymagane właściwości w treści żądania.</span><span class="sxs-lookup"><span data-stu-id="06695-124">This table describes the required properties in the request body.</span></span>

| <span data-ttu-id="06695-125">Nazwa</span><span class="sxs-lookup"><span data-stu-id="06695-125">Name</span></span>                              | <span data-ttu-id="06695-126">Typ</span><span class="sxs-lookup"><span data-stu-id="06695-126">Type</span></span>   | <span data-ttu-id="06695-127">Opis</span><span class="sxs-lookup"><span data-stu-id="06695-127">Description</span></span>                                 |
|------------------------------------------------------------------|--------|---------------------------------------------|
| [<span data-ttu-id="06695-128">SelfServePolicy</span><span class="sxs-lookup"><span data-stu-id="06695-128">SelfServePolicy</span></span>](self-serve-policy-resources.md#selfservepolicy)| <span data-ttu-id="06695-129">object</span><span class="sxs-lookup"><span data-stu-id="06695-129">object</span></span> | <span data-ttu-id="06695-130">Informacje o zasadach samoobsługi.</span><span class="sxs-lookup"><span data-stu-id="06695-130">The self-serve policy information.</span></span> |

#### <a name="selfservepolicy"></a><span data-ttu-id="06695-131">SelfServePolicy</span><span class="sxs-lookup"><span data-stu-id="06695-131">SelfServePolicy</span></span>

<span data-ttu-id="06695-132">Ta tabela zawiera opis minimalnych wymaganych pól z zasobów [SelfServePolicy](self-serve-policy-resources.md#selfservepolicy) wymaganych do utworzenia nowych zasad samoobsługi.</span><span class="sxs-lookup"><span data-stu-id="06695-132">This table describes the minimum required fields from the [SelfServePolicy](self-serve-policy-resources.md#selfservepolicy) resource needed to create a new self-serve policy.</span></span>

| <span data-ttu-id="06695-133">Właściwość</span><span class="sxs-lookup"><span data-stu-id="06695-133">Property</span></span>              | <span data-ttu-id="06695-134">Typ</span><span class="sxs-lookup"><span data-stu-id="06695-134">Type</span></span>             | <span data-ttu-id="06695-135">Opis</span><span class="sxs-lookup"><span data-stu-id="06695-135">Description</span></span>                                                                                            |
|-----------------------|------------------|--------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="06695-136">identyfikator</span><span class="sxs-lookup"><span data-stu-id="06695-136">id</span></span>                    | <span data-ttu-id="06695-137">ciąg</span><span class="sxs-lookup"><span data-stu-id="06695-137">string</span></span>           | <span data-ttu-id="06695-138">Identyfikator zasad samoobsługi, który jest dostarczany po pomyślnym utworzeniu zasad samoobsługi.</span><span class="sxs-lookup"><span data-stu-id="06695-138">A self-serve policy identifier that is supplied upon successful creation of the self-serve policy.</span></span>     |
| <span data-ttu-id="06695-139">SelfServeEntity</span><span class="sxs-lookup"><span data-stu-id="06695-139">SelfServeEntity</span></span>       | <span data-ttu-id="06695-140">SelfServeEntity</span><span class="sxs-lookup"><span data-stu-id="06695-140">SelfServeEntity</span></span>  | <span data-ttu-id="06695-141">Samoobsługowa jednostka, do której uzyskuje się dostęp.</span><span class="sxs-lookup"><span data-stu-id="06695-141">The self-serve entity that is being granted access.</span></span>                                                     |
| <span data-ttu-id="06695-142">Użytkownik udzielający uprawnienia</span><span class="sxs-lookup"><span data-stu-id="06695-142">Grantor</span></span>               | <span data-ttu-id="06695-143">Użytkownik udzielający uprawnienia</span><span class="sxs-lookup"><span data-stu-id="06695-143">Grantor</span></span>          | <span data-ttu-id="06695-144">Użytkownik udzielający uprawnienia udzielający dostępu.</span><span class="sxs-lookup"><span data-stu-id="06695-144">The grantor that is granting access.</span></span>                                                                    |
| <span data-ttu-id="06695-145">Uprawnienia</span><span class="sxs-lookup"><span data-stu-id="06695-145">Permissions</span></span>           | <span data-ttu-id="06695-146">Tablica uprawnień</span><span class="sxs-lookup"><span data-stu-id="06695-146">Array of Permission</span></span>| <span data-ttu-id="06695-147">Tablica zasobów [uprawnień](self-serve-policy-resources.md#permission) .</span><span class="sxs-lookup"><span data-stu-id="06695-147">An Array of [Permission](self-serve-policy-resources.md#permission) resources.</span></span>                                                      |
| <span data-ttu-id="06695-148">Element ETag</span><span class="sxs-lookup"><span data-stu-id="06695-148">Etag</span></span>                  | <span data-ttu-id="06695-149">ciąg</span><span class="sxs-lookup"><span data-stu-id="06695-149">string</span></span>           | <span data-ttu-id="06695-150">Element ETag.</span><span class="sxs-lookup"><span data-stu-id="06695-150">The Etag.</span></span>                                                                                               |


### <a name="request-example"></a><span data-ttu-id="06695-151">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="06695-151">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="06695-152">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="06695-152">REST response</span></span>

<span data-ttu-id="06695-153">Jeśli to się powiedzie, ten interfejs API zwraca zasób [SelfServePolicy](self-serve-policy-resources.md#selfservepolicy) dla zaktualizowanych zasad samoobsługi.</span><span class="sxs-lookup"><span data-stu-id="06695-153">If successful, this API returns a [SelfServePolicy](self-serve-policy-resources.md#selfservepolicy) resource for the updated self-serve policy.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="06695-154">Kody sukcesu i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="06695-154">Response success and error codes</span></span>

<span data-ttu-id="06695-155">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie i dodatkowe informacje debugowania.</span><span class="sxs-lookup"><span data-stu-id="06695-155">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="06695-156">Użyj narzędzia do śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="06695-156">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="06695-157">Aby uzyskać pełną listę, zobacz [kody błędów REST centrum partnera](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="06695-157">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

<span data-ttu-id="06695-158">Ta metoda zwraca następujące kody błędów:</span><span class="sxs-lookup"><span data-stu-id="06695-158">This method returns the following error codes:</span></span>

| <span data-ttu-id="06695-159">Kod stanu HTTP</span><span class="sxs-lookup"><span data-stu-id="06695-159">HTTP Status Code</span></span>     | <span data-ttu-id="06695-160">Kod błędu</span><span class="sxs-lookup"><span data-stu-id="06695-160">Error code</span></span>   | <span data-ttu-id="06695-161">Opis</span><span class="sxs-lookup"><span data-stu-id="06695-161">Description</span></span>                                                                |
|----------------------|--------------|----------------------------------------------------------------------------|
| <span data-ttu-id="06695-162">404</span><span class="sxs-lookup"><span data-stu-id="06695-162">404</span></span>                  | <span data-ttu-id="06695-163">600039</span><span class="sxs-lookup"><span data-stu-id="06695-163">600039</span></span>       | <span data-ttu-id="06695-164">Nie znaleziono zasad samoobsługi</span><span class="sxs-lookup"><span data-stu-id="06695-164">Self-serve policy was not found</span></span>                                            |
| <span data-ttu-id="06695-165">404</span><span class="sxs-lookup"><span data-stu-id="06695-165">404</span></span>                  | <span data-ttu-id="06695-166">600040</span><span class="sxs-lookup"><span data-stu-id="06695-166">600040</span></span>       | <span data-ttu-id="06695-167">Identyfikator zasad samoobsługi jest nieprawidłowy</span><span class="sxs-lookup"><span data-stu-id="06695-167">Self-serve policy identifier is incorrect</span></span>                                  |


### <a name="response-example"></a><span data-ttu-id="06695-168">Przykład odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="06695-168">Response example</span></span>

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
