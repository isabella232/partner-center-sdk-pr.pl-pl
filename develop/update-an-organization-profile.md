---
title: Aktualizowanie profilu organizacji
description: Aktualizuje profil rozliczeń w organizacji.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: ccf938fff285704f54d4717b2678e1419d857d8d
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/08/2020
ms.locfileid: "97767870"
---
# <a name="update-an-organization-profile"></a><span data-ttu-id="8aedd-103">Aktualizowanie profilu organizacji</span><span class="sxs-lookup"><span data-stu-id="8aedd-103">Update an organization profile</span></span>

<span data-ttu-id="8aedd-104">**Dotyczy**</span><span class="sxs-lookup"><span data-stu-id="8aedd-104">**Applies To**</span></span>

- <span data-ttu-id="8aedd-105">Centrum partnerskie</span><span class="sxs-lookup"><span data-stu-id="8aedd-105">Partner Center</span></span>
- <span data-ttu-id="8aedd-106">Centrum partnerskie obsługiwane przez firmę 21Vianet</span><span class="sxs-lookup"><span data-stu-id="8aedd-106">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="8aedd-107">Centrum partnerskie dla Microsoft Cloud Niemcy</span><span class="sxs-lookup"><span data-stu-id="8aedd-107">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="8aedd-108">Centrum partnerskie Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="8aedd-108">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="8aedd-109">Aktualizuje profil rozliczeń partnera.</span><span class="sxs-lookup"><span data-stu-id="8aedd-109">Updates a partner's billing profile.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8aedd-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="8aedd-110">Prerequisites</span></span>

- <span data-ttu-id="8aedd-111">Poświadczenia zgodnie z opisem w temacie [uwierzytelnianie w centrum partnerskim](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="8aedd-111">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="8aedd-112">Ten scenariusz obsługuje tylko uwierzytelnianie przy użyciu aplikacji i poświadczeń użytkownika.</span><span class="sxs-lookup"><span data-stu-id="8aedd-112">This scenario supports authentication with App+User credentials only.</span></span>

## <a name="c"></a><span data-ttu-id="8aedd-113">C\#</span><span class="sxs-lookup"><span data-stu-id="8aedd-113">C\#</span></span>

<span data-ttu-id="8aedd-114">Aby zaktualizować profil organizacji, należy pobrać profil i wprowadzić wymagane zmiany.</span><span class="sxs-lookup"><span data-stu-id="8aedd-114">To update your organization profile, retrieve the profile and make any necessary changes.</span></span> <span data-ttu-id="8aedd-115">Następnie użyj kolekcji **IAggregatePartner. profile** i Wywołaj Właściwość **OrganizationProfile** .</span><span class="sxs-lookup"><span data-stu-id="8aedd-115">Then, use your **IAggregatePartner.Profiles** collection and call the **OrganizationProfile** property.</span></span> <span data-ttu-id="8aedd-116">Na koniec Wywołaj metodę **Update ()** .</span><span class="sxs-lookup"><span data-stu-id="8aedd-116">Finally, call the **Update()** method.</span></span>

``` csharp
// IAggregatePartner partnerOperations;

OrganizationProfile organizationProfile = partnerOperations.Profiles.OrganizationProfile.Get();

// Generating a random phone number to update in the organization profile
organizationProfile.DefaultAddress.PhoneNumber = ((long)(new Random().NextDouble() * 9000000000) + 1000000000).ToString(CultureInfo.InvariantCulture);

OrganizationProfile updatedOrganizationProfile = partnerOperations.Profiles.OrganizationProfile.Update(organizationProfile);
```

<span data-ttu-id="8aedd-117">**Przykład**: [aplikacja testowa konsoli](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="8aedd-117">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="8aedd-118">**Project**: PartnerCenterSDK. FeaturesSamples **Klasa**: UpdateOrganizationProfile.cs</span><span class="sxs-lookup"><span data-stu-id="8aedd-118">**Project**: PartnerCenterSDK.FeaturesSamples **Class**: UpdateOrganizationProfile.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="8aedd-119">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="8aedd-119">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="8aedd-120">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="8aedd-120">Request syntax</span></span>

| <span data-ttu-id="8aedd-121">Metoda</span><span class="sxs-lookup"><span data-stu-id="8aedd-121">Method</span></span>  | <span data-ttu-id="8aedd-122">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="8aedd-122">Request URI</span></span>                                                                   |
|---------|-------------------------------------------------------------------------------|
| <span data-ttu-id="8aedd-123">**PUT**</span><span class="sxs-lookup"><span data-stu-id="8aedd-123">**PUT**</span></span> | <span data-ttu-id="8aedd-124">[*{baseURL}*](partner-center-rest-urls.md)/V1/Profiles/Organization http/1.1</span><span class="sxs-lookup"><span data-stu-id="8aedd-124">[*{baseURL}*](partner-center-rest-urls.md)/v1/profiles/organization HTTP/1.1</span></span> |

### <a name="request-headers"></a><span data-ttu-id="8aedd-125">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="8aedd-125">Request headers</span></span>

<span data-ttu-id="8aedd-126">Aby uzyskać więcej informacji, zobacz [nagłówki REST Centrum partnerskiego](headers.md).</span><span class="sxs-lookup"><span data-stu-id="8aedd-126">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="8aedd-127">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="8aedd-127">Request body</span></span>

<span data-ttu-id="8aedd-128">Brak.</span><span class="sxs-lookup"><span data-stu-id="8aedd-128">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="8aedd-129">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="8aedd-129">Request example</span></span>

```http
PUT https://api.partnercenter.microsoft.com/v1/profiles/organization HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: fe76387b-9658-47d7-939d-0c70032ef589
MS-CorrelationId: cb9f3209-d020-4bf9-871c-e1f1c75348f8
Content-Length: 624
Expect: 100-continue

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

## <a name="rest-response"></a><span data-ttu-id="8aedd-130">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="8aedd-130">REST response</span></span>

<span data-ttu-id="8aedd-131">Jeśli to się powiedzie, metoda zwraca obiekt **OrganizationProfile** w treści odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="8aedd-131">If successful, this method returns an **OrganizationProfile** object in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="8aedd-132">Kody sukcesu i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="8aedd-132">Response success and error codes</span></span>

<span data-ttu-id="8aedd-133">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie i dodatkowe informacje debugowania.</span><span class="sxs-lookup"><span data-stu-id="8aedd-133">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="8aedd-134">Użyj narzędzia do śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="8aedd-134">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="8aedd-135">Aby uzyskać pełną listę, zobacz [kody błędów](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="8aedd-135">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="8aedd-136">Przykład odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="8aedd-136">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 648
Content-Type: application/json; charset=utf-8
MS-CorrelationId: cb9f3209-d020-4bf9-871c-e1f1c75348f8
MS-RequestId: fe76387b-9658-47d7-939d-0c70032ef589
Date: Mon, 21 Mar 2016 05:48:41 GMT

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
