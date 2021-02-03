---
title: Pobieranie profilu organizacji
description: Pobiera obiekt reprezentujący profil organizacji partnera.
ms.date: 09/17/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: cychua
ms.author: cychua
ms.openlocfilehash: 132a1e0efa3efea69d4bf649e55b412e300b0685
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/19/2020
ms.locfileid: "97768453"
---
# <a name="get-an-organization-profile"></a><span data-ttu-id="202bb-103">Pobieranie profilu organizacji</span><span class="sxs-lookup"><span data-stu-id="202bb-103">Get an organization profile</span></span>

<span data-ttu-id="202bb-104">**Dotyczy**</span><span class="sxs-lookup"><span data-stu-id="202bb-104">**Applies To**</span></span>

- <span data-ttu-id="202bb-105">Centrum partnerskie</span><span class="sxs-lookup"><span data-stu-id="202bb-105">Partner Center</span></span>
- <span data-ttu-id="202bb-106">Centrum partnerskie obsługiwane przez firmę 21Vianet</span><span class="sxs-lookup"><span data-stu-id="202bb-106">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="202bb-107">Centrum partnerskie dla Microsoft Cloud Niemcy</span><span class="sxs-lookup"><span data-stu-id="202bb-107">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="202bb-108">Centrum partnerskie Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="202bb-108">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="202bb-109">Pobiera obiekt reprezentujący profil organizacji partnera.</span><span class="sxs-lookup"><span data-stu-id="202bb-109">Gets an object representing the partner's organization profile.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="202bb-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="202bb-110">Prerequisites</span></span>

- <span data-ttu-id="202bb-111">Poświadczenia zgodnie z opisem w temacie [uwierzytelnianie w centrum partnerskim](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="202bb-111">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="202bb-112">Ten scenariusz obsługuje tylko uwierzytelnianie przy użyciu aplikacji i poświadczeń użytkownika.</span><span class="sxs-lookup"><span data-stu-id="202bb-112">This scenario supports authentication with App+User credentials only.</span></span>

## <a name="c"></a><span data-ttu-id="202bb-113">C\#</span><span class="sxs-lookup"><span data-stu-id="202bb-113">C\#</span></span>

<span data-ttu-id="202bb-114">Aby uzyskać profil organizacji, Użyj kolekcji **IAggregatePartner. profile** i Wywołaj Właściwość **OrganizationProfile** .</span><span class="sxs-lookup"><span data-stu-id="202bb-114">To get your organization profile, use your **IAggregatePartner.Profiles** collection and call the **OrganizationProfile** property.</span></span> <span data-ttu-id="202bb-115">Na koniec wywołaj metody [**Get ()**](/dotnet/api/microsoft.store.partnercenter.profiles.iorganizationprofile.get) lub [**GetAsync ()**](/dotnet/api/microsoft.store.partnercenter.profiles.iorganizationprofile.getasync) .</span><span class="sxs-lookup"><span data-stu-id="202bb-115">Finally, call the [**Get()**](/dotnet/api/microsoft.store.partnercenter.profiles.iorganizationprofile.get) or [**GetAsync()**](/dotnet/api/microsoft.store.partnercenter.profiles.iorganizationprofile.getasync) methods.</span></span>

```csharp
// IAggregatePartner partnerOperations;

OrganizationProfile organizationProfile = partnerOperations.Profiles.OrganizationProfile.Get();
```

<span data-ttu-id="202bb-116">**Przykład**: [aplikacja testowa konsoli](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="202bb-116">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="202bb-117">**Project**: PartnerCenterSDK. FeaturesSamples **Klasa**: GetOrganizationProfile.cs</span><span class="sxs-lookup"><span data-stu-id="202bb-117">**Project**: PartnerCenterSDK.FeaturesSamples **Class**: GetOrganizationProfile.cs</span></span>

## <a name="java"></a><span data-ttu-id="202bb-118">Java</span><span class="sxs-lookup"><span data-stu-id="202bb-118">Java</span></span>

[!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

<span data-ttu-id="202bb-119">Aby uzyskać profil organizacji, użyj funkcji **IAggregatePartner. Getprofiles** i wywołaj funkcję **getOrganizationProfile** .</span><span class="sxs-lookup"><span data-stu-id="202bb-119">To get your organization profile, use your **IAggregatePartner.getProfiles** function and call the **getOrganizationProfile** function.</span></span> <span data-ttu-id="202bb-120">Na koniec wywołaj funkcję **Get ()** .</span><span class="sxs-lookup"><span data-stu-id="202bb-120">Finally, call the **get()** function.</span></span>

```java
// IAggregatePartner partnerOperations;

OrganizationProfile organizationProfile = partnerOperations.getProfiles().getOrganizationProfile().get();
```

## <a name="powershell"></a><span data-ttu-id="202bb-121">PowerShell</span><span class="sxs-lookup"><span data-stu-id="202bb-121">PowerShell</span></span>

[!INCLUDE [Partner Center PowerShell module support details](../includes/powershell-module-support.md)]

<span data-ttu-id="202bb-122">Aby uzyskać profil organizacji, uruchom polecenie [**Get-PartnerOrganizationProfile**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerOrganizationProfile.md) .</span><span class="sxs-lookup"><span data-stu-id="202bb-122">To get your organization profile, execute the [**Get-PartnerOrganizationProfile**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerOrganizationProfile.md) command.</span></span>

```powershell
Get-PartnerOrganizationProfile
```

## <a name="rest-request"></a><span data-ttu-id="202bb-123">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="202bb-123">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="202bb-124">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="202bb-124">Request syntax</span></span>

| <span data-ttu-id="202bb-125">Metoda</span><span class="sxs-lookup"><span data-stu-id="202bb-125">Method</span></span>  | <span data-ttu-id="202bb-126">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="202bb-126">Request URI</span></span>                                                                   |
|---------|-------------------------------------------------------------------------------|
| <span data-ttu-id="202bb-127">**Pobierz**</span><span class="sxs-lookup"><span data-stu-id="202bb-127">**GET**</span></span> | <span data-ttu-id="202bb-128">[*{baseURL}*](partner-center-rest-urls.md)/V1/Profiles/Organization http/1.1</span><span class="sxs-lookup"><span data-stu-id="202bb-128">[*{baseURL}*](partner-center-rest-urls.md)/v1/profiles/organization HTTP/1.1</span></span> |

### <a name="request-headers"></a><span data-ttu-id="202bb-129">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="202bb-129">Request headers</span></span>

<span data-ttu-id="202bb-130">Aby uzyskać więcej informacji, zobacz [nagłówki REST Centrum partnerskiego](headers.md).</span><span class="sxs-lookup"><span data-stu-id="202bb-130">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="202bb-131">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="202bb-131">Request body</span></span>

<span data-ttu-id="202bb-132">Brak.</span><span class="sxs-lookup"><span data-stu-id="202bb-132">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="202bb-133">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="202bb-133">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/profiles/organization HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: b85cb7ab-cc2e-4966-93f0-cf0d8377a93f
MS-CorrelationId: 1bb03149-88d2-4bc2-9cc1-d6e83890fa9e
```

## <a name="rest-response"></a><span data-ttu-id="202bb-134">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="202bb-134">REST response</span></span>

<span data-ttu-id="202bb-135">Jeśli to się powiedzie, metoda zwraca obiekt **OrganizationProfile** w treści odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="202bb-135">If successful, this method returns an **OrganizationProfile** object in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="202bb-136">Kody sukcesu i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="202bb-136">Response success and error codes</span></span>

<span data-ttu-id="202bb-137">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie i dodatkowe informacje debugowania.</span><span class="sxs-lookup"><span data-stu-id="202bb-137">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="202bb-138">Użyj narzędzia do śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="202bb-138">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="202bb-139">Aby uzyskać pełną listę, zobacz [kody błędów](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="202bb-139">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="202bb-140">Przykład odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="202bb-140">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 648
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 1bb03149-88d2-4bc2-9cc1-d6e83890fa9e
MS-RequestId: b85cb7ab-cc2e-4966-93f0-cf0d8377a93f
Date: Tue, 22 Mar 2016 17:11:06 GMT

{
    "id":<id>,
    "companyName":"TEST_TEST_BugBash1",
    "defaultAddress":{
        "country":"US",
        "city":"Redmond",
        "state":"WA",
        "addressLine1":"Two Microsoft Way",
        "addressLine2":"",
        "postalCode":"98052",
        "firstName":"Test",
        "lastName":"Account",
        "phoneNumber":""
    },
    "tenantId":<tenantID>,
    "domain":"testtestbugbash1.onmicrosoft.com",
    "email":"test-partner@microsoft.com",
    "language":"es",
    "culture":"es-US",
    "profileType":"OrganizationProfile",
    "links":{
        "self":{
            "uri":"/profiles/organization",
            "method":"GET",
            "headers":[]
        }
    },
    "attributes":{
        "etag":<etag>,
        "objectType":"OrganizationProfile"
    }
}
```
