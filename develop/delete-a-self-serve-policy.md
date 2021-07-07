---
title: Usuwanie zasad samoobsługi
description: Jak usunąć zasady samoobsługi.
ms.date: 04/13/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 063cf98d4c78e82622e486427baeb1a5721715e5
ms.sourcegitcommit: ad8082bee01fb1f57da423b417ca1ca9c0df8e45
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/10/2021
ms.locfileid: "111973098"
---
# <a name="delete-a-selfservepolicy"></a><span data-ttu-id="b9166-103">Usuwanie samoobsługi (SelfServePolicy)</span><span class="sxs-lookup"><span data-stu-id="b9166-103">Delete a SelfServePolicy</span></span>

<span data-ttu-id="b9166-104">W tym artykule wyjaśniono, jak zaktualizować zasady samoobsługi.</span><span class="sxs-lookup"><span data-stu-id="b9166-104">This article explains how to update a self-serve policy.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b9166-105">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="b9166-105">Prerequisites</span></span>

- <span data-ttu-id="b9166-106">Poświadczenia zgodnie z opisem w te [Partner Center uwierzytelniania.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="b9166-106">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="b9166-107">Ten scenariusz obsługuje uwierzytelnianie przy użyciu poświadczeń aplikacji i użytkownika.</span><span class="sxs-lookup"><span data-stu-id="b9166-107">This scenario supports authentication with Application+User credentials.</span></span>

## <a name="c"></a><span data-ttu-id="b9166-108">C\#</span><span class="sxs-lookup"><span data-stu-id="b9166-108">C\#</span></span>

<span data-ttu-id="b9166-109">Aby usunąć zasady samoobsługi:</span><span class="sxs-lookup"><span data-stu-id="b9166-109">To delete a self-serve policy:</span></span>

1. <span data-ttu-id="b9166-110">Wywołaj [**metodę IAggregatePartner.SelfServePolicies.ById**](/dotnet/api/microsoft.store.partnercenter.iselfservepoliciescollection.byid) z identyfikatorem jednostki, aby pobrać interfejs do operacji na zasadach.</span><span class="sxs-lookup"><span data-stu-id="b9166-110">Call the [**IAggregatePartner.SelfServePolicies.ById**](/dotnet/api/microsoft.store.partnercenter.iselfservepoliciescollection.byid) method with the entity identifier to retrieve an interface to operations on the policies.</span></span>

2. <span data-ttu-id="b9166-111">Wywołaj [**metodę Delete**](/dotnet/api/microsoft.store.partnercenter.SelfServePolicies.delete) lub [**DeleteAsync,**](/dotnet/api/microsoft.store.partnercenter.SelfServePolicies.deleteasync) aby usunąć zasady samoobsługi.</span><span class="sxs-lookup"><span data-stu-id="b9166-111">Call the [**Delete**](/dotnet/api/microsoft.store.partnercenter.SelfServePolicies.delete) or [**DeleteAsync**](/dotnet/api/microsoft.store.partnercenter.SelfServePolicies.deleteasync) method to delete the self-serve policy.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
string policyId;

// All the operations executed on this partner operation instance will share the same correlation Id but will differ in request Id
IPartner scopedPartnerOperations = partnerOperations.With(RequestContextFactory.Instance.Create(Guid.NewGuid()));

// deletes the self-serve policies
partnerOperations.SelfServePolicies.ById(policyId).Delete();
```

<span data-ttu-id="b9166-112">Przykład można znaleźć w następujących tematach:</span><span class="sxs-lookup"><span data-stu-id="b9166-112">For an example, see the following:</span></span>

- <span data-ttu-id="b9166-113">Przykład: [aplikacja testowa konsoli](console-test-app.md)</span><span class="sxs-lookup"><span data-stu-id="b9166-113">Sample: [Console test app](console-test-app.md)</span></span>
- <span data-ttu-id="b9166-114">Project: **PartnerSDK.FeatureSamples**</span><span class="sxs-lookup"><span data-stu-id="b9166-114">Project: **PartnerSDK.FeatureSamples**</span></span>
- <span data-ttu-id="b9166-115">Klasa: **DeleteSelfServePolicies.cs**</span><span class="sxs-lookup"><span data-stu-id="b9166-115">Class: **DeleteSelfServePolicies.cs**</span></span>

## <a name="rest-request"></a><span data-ttu-id="b9166-116">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="b9166-116">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="b9166-117">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="b9166-117">Request syntax</span></span>

| <span data-ttu-id="b9166-118">Metoda</span><span class="sxs-lookup"><span data-stu-id="b9166-118">Method</span></span>  | <span data-ttu-id="b9166-119">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="b9166-119">Request URI</span></span>                                                                   |
|---------|-------------------------------------------------------------------------------|
| <span data-ttu-id="b9166-120">**Usunąć**</span><span class="sxs-lookup"><span data-stu-id="b9166-120">**DELETE**</span></span> | <span data-ttu-id="b9166-121">[*{baseURL}*](partner-center-rest-urls.md)/v1/SelfServePolicy/{id} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="b9166-121">[*{baseURL}*](partner-center-rest-urls.md)/v1/SelfServePolicy/{id} HTTP/1.1</span></span> |

<span data-ttu-id="b9166-122">**Parametr URI**</span><span class="sxs-lookup"><span data-stu-id="b9166-122">**URI parameter**</span></span>

<span data-ttu-id="b9166-123">Użyj następujących parametrów ścieżki, aby uzyskać określony produkt.</span><span class="sxs-lookup"><span data-stu-id="b9166-123">Use the following path parameters to get the specified product.</span></span>

| <span data-ttu-id="b9166-124">Nazwa</span><span class="sxs-lookup"><span data-stu-id="b9166-124">Name</span></span>                       | <span data-ttu-id="b9166-125">Typ</span><span class="sxs-lookup"><span data-stu-id="b9166-125">Type</span></span>         | <span data-ttu-id="b9166-126">Wymagane</span><span class="sxs-lookup"><span data-stu-id="b9166-126">Required</span></span> | <span data-ttu-id="b9166-127">Opis</span><span class="sxs-lookup"><span data-stu-id="b9166-127">Description</span></span>                                                     |
|----------------------------|--------------|----------|-----------------------------------------------------------------|
| <span data-ttu-id="b9166-128">**SelfServePolicy-id**</span><span class="sxs-lookup"><span data-stu-id="b9166-128">**SelfServePolicy-id**</span></span>     | <span data-ttu-id="b9166-129">**ciąg**</span><span class="sxs-lookup"><span data-stu-id="b9166-129">**string**</span></span>   | <span data-ttu-id="b9166-130">Tak</span><span class="sxs-lookup"><span data-stu-id="b9166-130">Yes</span></span>      | <span data-ttu-id="b9166-131">Ciąg, który identyfikuje zasady samoobsługi.</span><span class="sxs-lookup"><span data-stu-id="b9166-131">A string that identifies the self-serve policy.</span></span>                 |

### <a name="request-headers"></a><span data-ttu-id="b9166-132">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="b9166-132">Request headers</span></span>

- <span data-ttu-id="b9166-133">Wymagany jest identyfikator żądania i identyfikator korelacji.</span><span class="sxs-lookup"><span data-stu-id="b9166-133">A request ID and correlation ID are required.</span></span>
- <span data-ttu-id="b9166-134">Aby uzyskać więcej informacji, [zobacz Partner Center REST headers (Nagłówki REST).](headers.md)</span><span class="sxs-lookup"><span data-stu-id="b9166-134">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="b9166-135">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="b9166-135">Request body</span></span>

<span data-ttu-id="b9166-136">Brak.</span><span class="sxs-lookup"><span data-stu-id="b9166-136">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="b9166-137">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="b9166-137">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="b9166-138">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="b9166-138">REST response</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="b9166-139">Kody powodzenia i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="b9166-139">Response success and error codes</span></span>

<span data-ttu-id="b9166-140">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie, oraz dodatkowe informacje o debugowaniu.</span><span class="sxs-lookup"><span data-stu-id="b9166-140">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="b9166-141">Użyj narzędzia śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="b9166-141">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="b9166-142">Aby uzyskać pełną listę, zobacz [Partner Center kodów błędów REST.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="b9166-142">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="b9166-143">Przykład odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="b9166-143">Response example</span></span>

```http
HTTP/1.1 204 deleted
MS-CorrelationId: ab993325-1605-4cf4-bac4-fb584142a31b
MS-RequestId: 94e4e214-6b06-4fb7-96d1-94d559f9b47f
Date: Tue, 14 Feb 2017 20:06:02 GMT

```
