---
title: Pobieranie profilu organizacji
description: Pobiera obiekt reprezentujący profil organizacji partnera.
ms.date: 09/17/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: cychua
ms.author: cychua
ms.openlocfilehash: 1c7272761612e573388d4facea1a78808a5bad52
ms.sourcegitcommit: d4b0c80d81f1d5bdf3c4c03344ad639646ae6ab9
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/09/2021
ms.locfileid: "111760559"
---
# <a name="get-an-organization-profile"></a><span data-ttu-id="ab993-103">Pobieranie profilu organizacji</span><span class="sxs-lookup"><span data-stu-id="ab993-103">Get an organization profile</span></span>

<span data-ttu-id="ab993-104">**Dotyczy:** Partner Center | Partner Center obsługiwana przez firmę 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="ab993-104">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="ab993-105">Pobiera obiekt reprezentujący profil organizacji partnera.</span><span class="sxs-lookup"><span data-stu-id="ab993-105">Gets an object representing the partner's organization profile.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ab993-106">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="ab993-106">Prerequisites</span></span>

- <span data-ttu-id="ab993-107">Poświadczenia zgodnie z opisem w [te Partner Center uwierzytelniania.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="ab993-107">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="ab993-108">Ten scenariusz obsługuje uwierzytelnianie tylko przy użyciu poświadczeń aplikacji i użytkownika.</span><span class="sxs-lookup"><span data-stu-id="ab993-108">This scenario supports authentication with App+User credentials only.</span></span>

## <a name="c"></a><span data-ttu-id="ab993-109">C\#</span><span class="sxs-lookup"><span data-stu-id="ab993-109">C\#</span></span>

<span data-ttu-id="ab993-110">Aby uzyskać profil organizacji, użyj **kolekcji IAggregatePartner.Profiles** i wywołaj **właściwość OrganizationProfile.**</span><span class="sxs-lookup"><span data-stu-id="ab993-110">To get your organization profile, use your **IAggregatePartner.Profiles** collection and call the **OrganizationProfile** property.</span></span> <span data-ttu-id="ab993-111">Na koniec wywołaj [**metody Get()**](/dotnet/api/microsoft.store.partnercenter.profiles.iorganizationprofile.get) [**lub GetAsync().**](/dotnet/api/microsoft.store.partnercenter.profiles.iorganizationprofile.getasync)</span><span class="sxs-lookup"><span data-stu-id="ab993-111">Finally, call the [**Get()**](/dotnet/api/microsoft.store.partnercenter.profiles.iorganizationprofile.get) or [**GetAsync()**](/dotnet/api/microsoft.store.partnercenter.profiles.iorganizationprofile.getasync) methods.</span></span>

```csharp
// IAggregatePartner partnerOperations;

OrganizationProfile organizationProfile = partnerOperations.Profiles.OrganizationProfile.Get();
```

<span data-ttu-id="ab993-112">**Przykład:** [aplikacja testowa konsoli](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="ab993-112">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="ab993-113">**Project:** PartnerCenterSDK.FeaturesSamples, **klasa**: GetOrganizationProfile.cs</span><span class="sxs-lookup"><span data-stu-id="ab993-113">**Project**: PartnerCenterSDK.FeaturesSamples **Class**: GetOrganizationProfile.cs</span></span>

## <a name="java"></a><span data-ttu-id="ab993-114">Java</span><span class="sxs-lookup"><span data-stu-id="ab993-114">Java</span></span>

[!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

<span data-ttu-id="ab993-115">Aby uzyskać profil organizacji, użyj funkcji **IAggregatePartner.getProfiles** i wywołaj funkcję **getOrganizationProfile.**</span><span class="sxs-lookup"><span data-stu-id="ab993-115">To get your organization profile, use your **IAggregatePartner.getProfiles** function and call the **getOrganizationProfile** function.</span></span> <span data-ttu-id="ab993-116">Na koniec wywołaj **funkcję get().**</span><span class="sxs-lookup"><span data-stu-id="ab993-116">Finally, call the **get()** function.</span></span>

```java
// IAggregatePartner partnerOperations;

OrganizationProfile organizationProfile = partnerOperations.getProfiles().getOrganizationProfile().get();
```

## <a name="powershell"></a><span data-ttu-id="ab993-117">PowerShell</span><span class="sxs-lookup"><span data-stu-id="ab993-117">PowerShell</span></span>

[!INCLUDE [Partner Center PowerShell module support details](../includes/powershell-module-support.md)]

<span data-ttu-id="ab993-118">Aby uzyskać profil organizacji, wykonaj polecenie [**Get-PartnerOrganizationProfile.**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerOrganizationProfile.md)</span><span class="sxs-lookup"><span data-stu-id="ab993-118">To get your organization profile, execute the [**Get-PartnerOrganizationProfile**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerOrganizationProfile.md) command.</span></span>

```powershell
Get-PartnerOrganizationProfile
```

## <a name="rest-request"></a><span data-ttu-id="ab993-119">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="ab993-119">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="ab993-120">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="ab993-120">Request syntax</span></span>

| <span data-ttu-id="ab993-121">Metoda</span><span class="sxs-lookup"><span data-stu-id="ab993-121">Method</span></span>  | <span data-ttu-id="ab993-122">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="ab993-122">Request URI</span></span>                                                                   |
|---------|-------------------------------------------------------------------------------|
| <span data-ttu-id="ab993-123">**Pobierz**</span><span class="sxs-lookup"><span data-stu-id="ab993-123">**GET**</span></span> | <span data-ttu-id="ab993-124">[*{baseURL}*](partner-center-rest-urls.md)/v1/profiles/organization HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="ab993-124">[*{baseURL}*](partner-center-rest-urls.md)/v1/profiles/organization HTTP/1.1</span></span> |

### <a name="request-headers"></a><span data-ttu-id="ab993-125">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="ab993-125">Request headers</span></span>

<span data-ttu-id="ab993-126">Aby uzyskać więcej informacji, [zobacz Partner Center REST headers (Nagłówki REST).](headers.md)</span><span class="sxs-lookup"><span data-stu-id="ab993-126">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="ab993-127">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="ab993-127">Request body</span></span>

<span data-ttu-id="ab993-128">Brak.</span><span class="sxs-lookup"><span data-stu-id="ab993-128">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="ab993-129">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="ab993-129">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/profiles/organization HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: b85cb7ab-cc2e-4966-93f0-cf0d8377a93f
MS-CorrelationId: 1bb03149-88d2-4bc2-9cc1-d6e83890fa9e
```

## <a name="rest-response"></a><span data-ttu-id="ab993-130">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="ab993-130">REST response</span></span>

<span data-ttu-id="ab993-131">W przypadku powodzenia ta metoda zwraca obiekt **OrganizationProfile** w treści odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="ab993-131">If successful, this method returns an **OrganizationProfile** object in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="ab993-132">Kody powodzenia i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="ab993-132">Response success and error codes</span></span>

<span data-ttu-id="ab993-133">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie, oraz dodatkowe informacje o debugowaniu.</span><span class="sxs-lookup"><span data-stu-id="ab993-133">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="ab993-134">Użyj narzędzia śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="ab993-134">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="ab993-135">Aby uzyskać pełną listę, zobacz [Kody błędów](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="ab993-135">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="ab993-136">Przykład odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="ab993-136">Response example</span></span>

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
