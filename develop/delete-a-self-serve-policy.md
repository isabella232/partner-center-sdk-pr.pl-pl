---
title: Usuwanie zasad samoobsługi
description: Jak usunąć zasady samoobsługowe.
ms.date: 04/13/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 3450145d6daf2ffca5e2886245e592406cb0886d
ms.sourcegitcommit: 01e75175077611da92175c777a440a594fb05797
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/08/2020
ms.locfileid: "97770227"
---
# <a name="delete-a-selfservepolicy"></a><span data-ttu-id="3b3ad-103">Usuń SelfServePolicy</span><span class="sxs-lookup"><span data-stu-id="3b3ad-103">Delete a SelfServePolicy</span></span>

<span data-ttu-id="3b3ad-104">**Dotyczy:**</span><span class="sxs-lookup"><span data-stu-id="3b3ad-104">**Applies to:**</span></span>

- <span data-ttu-id="3b3ad-105">Centrum partnerskie</span><span class="sxs-lookup"><span data-stu-id="3b3ad-105">Partner Center</span></span>

<span data-ttu-id="3b3ad-106">W tym temacie opisano sposób aktualizowania zasad samoobsługi.</span><span class="sxs-lookup"><span data-stu-id="3b3ad-106">This topic explains how to update a self-serve policy.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3b3ad-107">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="3b3ad-107">Prerequisites</span></span>

- <span data-ttu-id="3b3ad-108">Poświadczenia zgodnie z opisem w temacie [uwierzytelnianie w centrum partnerskim](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="3b3ad-108">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="3b3ad-109">Ten scenariusz obsługuje uwierzytelnianie przy użyciu poświadczeń aplikacji i użytkownika.</span><span class="sxs-lookup"><span data-stu-id="3b3ad-109">This scenario supports authentication with Application+User credentials.</span></span>

## <a name="c"></a><span data-ttu-id="3b3ad-110">C\#</span><span class="sxs-lookup"><span data-stu-id="3b3ad-110">C\#</span></span>

<span data-ttu-id="3b3ad-111">Aby usunąć zasady samoobsługowe:</span><span class="sxs-lookup"><span data-stu-id="3b3ad-111">To delete a self-serve policy:</span></span>

1. <span data-ttu-id="3b3ad-112">Wywołaj metodę [**IAggregatePartner. SelfServePolicies. ById**](/dotnet/api/microsoft.store.partnercenter.iselfservepoliciescollection.byid) z identyfikatorem jednostki, aby pobrać interfejs do operacji w ramach zasad.</span><span class="sxs-lookup"><span data-stu-id="3b3ad-112">Call the [**IAggregatePartner.SelfServePolicies.ById**](/dotnet/api/microsoft.store.partnercenter.iselfservepoliciescollection.byid) method with the entity identifier to retrieve an interface to operations on the policies.</span></span>

2. <span data-ttu-id="3b3ad-113">Wywołaj metodę [**delete**](/dotnet/api/microsoft.store.partnercenter.SelfServePolicies.delete) lub [**DeleteAsync**](/dotnet/api/microsoft.store.partnercenter.SelfServePolicies.deleteasync) , aby usunąć zasady samoobsługi.</span><span class="sxs-lookup"><span data-stu-id="3b3ad-113">Call the [**Delete**](/dotnet/api/microsoft.store.partnercenter.SelfServePolicies.delete) or [**DeleteAsync**](/dotnet/api/microsoft.store.partnercenter.SelfServePolicies.deleteasync) method to delete the self-serve policy.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
string policyId;

// All the operations executed on this partner operation instance will share the same correlation Id but will differ in request Id
IPartner scopedPartnerOperations = partnerOperations.With(RequestContextFactory.Instance.Create(Guid.NewGuid()));

// deletes the self-serve policies
partnerOperations.SelfServePolicies.ById(policyId).Delete();
```

<span data-ttu-id="3b3ad-114">Aby zapoznać się z przykładem, zobacz następujące tematy:</span><span class="sxs-lookup"><span data-stu-id="3b3ad-114">For an example, see the following:</span></span>

- <span data-ttu-id="3b3ad-115">Przykład: [aplikacja testowa konsoli](console-test-app.md)</span><span class="sxs-lookup"><span data-stu-id="3b3ad-115">Sample: [Console test app](console-test-app.md)</span></span>
- <span data-ttu-id="3b3ad-116">Projekt: **PartnerSDK. FeatureSamples**</span><span class="sxs-lookup"><span data-stu-id="3b3ad-116">Project: **PartnerSDK.FeatureSamples**</span></span>
- <span data-ttu-id="3b3ad-117">Klasa: **DeleteSelfServePolicies.cs**</span><span class="sxs-lookup"><span data-stu-id="3b3ad-117">Class: **DeleteSelfServePolicies.cs**</span></span>

## <a name="rest-request"></a><span data-ttu-id="3b3ad-118">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="3b3ad-118">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="3b3ad-119">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="3b3ad-119">Request syntax</span></span>

| <span data-ttu-id="3b3ad-120">Metoda</span><span class="sxs-lookup"><span data-stu-id="3b3ad-120">Method</span></span>  | <span data-ttu-id="3b3ad-121">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="3b3ad-121">Request URI</span></span>                                                                   |
|---------|-------------------------------------------------------------------------------|
| <span data-ttu-id="3b3ad-122">**USUNIĘTY**</span><span class="sxs-lookup"><span data-stu-id="3b3ad-122">**DELETE**</span></span> | <span data-ttu-id="3b3ad-123">[*{baseURL}*](partner-center-rest-urls.md)/V1/SelfServePolicy/{ID} http/1.1</span><span class="sxs-lookup"><span data-stu-id="3b3ad-123">[*{baseURL}*](partner-center-rest-urls.md)/v1/SelfServePolicy/{id} HTTP/1.1</span></span> |

<span data-ttu-id="3b3ad-124">**Parametr URI**</span><span class="sxs-lookup"><span data-stu-id="3b3ad-124">**URI parameter**</span></span>

<span data-ttu-id="3b3ad-125">Aby uzyskać określony produkt, użyj następujących parametrów ścieżki.</span><span class="sxs-lookup"><span data-stu-id="3b3ad-125">Use the following path parameters to get the specified product.</span></span>

| <span data-ttu-id="3b3ad-126">Nazwa</span><span class="sxs-lookup"><span data-stu-id="3b3ad-126">Name</span></span>                       | <span data-ttu-id="3b3ad-127">Typ</span><span class="sxs-lookup"><span data-stu-id="3b3ad-127">Type</span></span>         | <span data-ttu-id="3b3ad-128">Wymagane</span><span class="sxs-lookup"><span data-stu-id="3b3ad-128">Required</span></span> | <span data-ttu-id="3b3ad-129">Opis</span><span class="sxs-lookup"><span data-stu-id="3b3ad-129">Description</span></span>                                                     |
|----------------------------|--------------|----------|-----------------------------------------------------------------|
| <span data-ttu-id="3b3ad-130">**SelfServePolicy — identyfikator**</span><span class="sxs-lookup"><span data-stu-id="3b3ad-130">**SelfServePolicy-id**</span></span>     | <span data-ttu-id="3b3ad-131">**parametry**</span><span class="sxs-lookup"><span data-stu-id="3b3ad-131">**string**</span></span>   | <span data-ttu-id="3b3ad-132">Tak</span><span class="sxs-lookup"><span data-stu-id="3b3ad-132">Yes</span></span>      | <span data-ttu-id="3b3ad-133">Ciąg identyfikujący zasady samoobsługi.</span><span class="sxs-lookup"><span data-stu-id="3b3ad-133">A string that identifies the self-serve policy.</span></span>                 |

### <a name="request-headers"></a><span data-ttu-id="3b3ad-134">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="3b3ad-134">Request headers</span></span>

- <span data-ttu-id="3b3ad-135">Identyfikator żądania i identyfikator korelacji są wymagane.</span><span class="sxs-lookup"><span data-stu-id="3b3ad-135">A request ID and correlation ID are required.</span></span>
- <span data-ttu-id="3b3ad-136">Aby uzyskać więcej informacji, zobacz [nagłówki REST Centrum partnerskiego](headers.md) .</span><span class="sxs-lookup"><span data-stu-id="3b3ad-136">See [Partner Center REST headers](headers.md) for more information.</span></span>

### <a name="request-body"></a><span data-ttu-id="3b3ad-137">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="3b3ad-137">Request body</span></span>

<span data-ttu-id="3b3ad-138">Brak.</span><span class="sxs-lookup"><span data-stu-id="3b3ad-138">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="3b3ad-139">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="3b3ad-139">Request example</span></span>

```http
DELETE https://api.partnercenter.microsoft.com/v1/SelfServePolicy/634f6379-ad54-449b-9821-564f737158ab_0431a72c-7d8a-4393-b25e-ef63f5efb415 HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 94e4e214-6b06-4fb7-96d1-94d559f9b47f
MS-CorrelationId: ab993325-1605-4cf4-bac4-fb584142a31b
X-Locale: en-US
Host: api.partnercenter.microsoft.com
Content-Length: 789
Connection: Keep-Alive

```

## <a name="rest-response"></a><span data-ttu-id="3b3ad-140">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="3b3ad-140">REST response</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="3b3ad-141">Kody sukcesu i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="3b3ad-141">Response success and error codes</span></span>

<span data-ttu-id="3b3ad-142">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie i dodatkowe informacje debugowania.</span><span class="sxs-lookup"><span data-stu-id="3b3ad-142">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="3b3ad-143">Użyj narzędzia do śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="3b3ad-143">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="3b3ad-144">Aby uzyskać pełną listę, zobacz [kody błędów REST centrum partnera](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="3b3ad-144">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="3b3ad-145">Przykład odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="3b3ad-145">Response example</span></span>

```http
HTTP/1.1 204 deleted
MS-CorrelationId: ab993325-1605-4cf4-bac4-fb584142a31b
MS-RequestId: 94e4e214-6b06-4fb7-96d1-94d559f9b47f
Date: Tue, 14 Feb 2017 20:06:02 GMT

```
