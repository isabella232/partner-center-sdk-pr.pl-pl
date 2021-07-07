---
title: Aktualizowanie profilu organizacji
description: Aktualizuje profil rozliczeniowy organizacji.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 0ef736a722cde16f95ed6dfdbdab278c98fcf738
ms.sourcegitcommit: 4275f9f67f9479ce27af6a9fda96fe86d0bc0b44
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/05/2021
ms.locfileid: "111530059"
---
# <a name="update-an-organization-profile"></a><span data-ttu-id="44e1c-103">Aktualizowanie profilu organizacji</span><span class="sxs-lookup"><span data-stu-id="44e1c-103">Update an organization profile</span></span>

<span data-ttu-id="44e1c-104">**Dotyczy:** Partner Center | Partner Center obsługiwana przez firmę 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="44e1c-104">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="44e1c-105">Aktualizuje profil rozliczeniowy partnera.</span><span class="sxs-lookup"><span data-stu-id="44e1c-105">Updates a partner's billing profile.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="44e1c-106">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="44e1c-106">Prerequisites</span></span>

- <span data-ttu-id="44e1c-107">Poświadczenia zgodnie z opisem w te [Partner Center uwierzytelniania.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="44e1c-107">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="44e1c-108">Ten scenariusz obsługuje uwierzytelnianie tylko przy użyciu poświadczeń aplikacji i użytkownika.</span><span class="sxs-lookup"><span data-stu-id="44e1c-108">This scenario supports authentication with App+User credentials only.</span></span>

## <a name="c"></a><span data-ttu-id="44e1c-109">C\#</span><span class="sxs-lookup"><span data-stu-id="44e1c-109">C\#</span></span>

<span data-ttu-id="44e1c-110">Aby zaktualizować profil organizacji, pobierz profil i dokonaj wszelkich niezbędnych zmian.</span><span class="sxs-lookup"><span data-stu-id="44e1c-110">To update your organization profile, retrieve the profile and make any necessary changes.</span></span> <span data-ttu-id="44e1c-111">Następnie użyj **kolekcji IAggregatePartner.Profiles** i wywołaj właściwość **OrganizationProfile.**</span><span class="sxs-lookup"><span data-stu-id="44e1c-111">Then, use your **IAggregatePartner.Profiles** collection and call the **OrganizationProfile** property.</span></span> <span data-ttu-id="44e1c-112">Na koniec wywołaj **metodę Update().**</span><span class="sxs-lookup"><span data-stu-id="44e1c-112">Finally, call the **Update()** method.</span></span>

``` csharp
// IAggregatePartner partnerOperations;

OrganizationProfile organizationProfile = partnerOperations.Profiles.OrganizationProfile.Get();

// Generating a random phone number to update in the organization profile
organizationProfile.DefaultAddress.PhoneNumber = ((long)(new Random().NextDouble() * 9000000000) + 1000000000).ToString(CultureInfo.InvariantCulture);

OrganizationProfile updatedOrganizationProfile = partnerOperations.Profiles.OrganizationProfile.Update(organizationProfile);
```

<span data-ttu-id="44e1c-113">**Przykład:** [aplikacja testowa konsoli](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="44e1c-113">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="44e1c-114">**Project:** PartnerCenterSDK.FeaturesSamples, **klasa:** UpdateOrganizationProfile.cs</span><span class="sxs-lookup"><span data-stu-id="44e1c-114">**Project**: PartnerCenterSDK.FeaturesSamples **Class**: UpdateOrganizationProfile.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="44e1c-115">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="44e1c-115">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="44e1c-116">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="44e1c-116">Request syntax</span></span>

| <span data-ttu-id="44e1c-117">Metoda</span><span class="sxs-lookup"><span data-stu-id="44e1c-117">Method</span></span>  | <span data-ttu-id="44e1c-118">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="44e1c-118">Request URI</span></span>                                                                   |
|---------|-------------------------------------------------------------------------------|
| <span data-ttu-id="44e1c-119">**PUT**</span><span class="sxs-lookup"><span data-stu-id="44e1c-119">**PUT**</span></span> | <span data-ttu-id="44e1c-120">[*{baseURL}*](partner-center-rest-urls.md)/v1/profiles/organization HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="44e1c-120">[*{baseURL}*](partner-center-rest-urls.md)/v1/profiles/organization HTTP/1.1</span></span> |

### <a name="request-headers"></a><span data-ttu-id="44e1c-121">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="44e1c-121">Request headers</span></span>

<span data-ttu-id="44e1c-122">Aby uzyskać więcej informacji, [zobacz Partner Center REST headers (Nagłówki REST).](headers.md)</span><span class="sxs-lookup"><span data-stu-id="44e1c-122">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="44e1c-123">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="44e1c-123">Request body</span></span>

<span data-ttu-id="44e1c-124">Brak.</span><span class="sxs-lookup"><span data-stu-id="44e1c-124">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="44e1c-125">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="44e1c-125">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="44e1c-126">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="44e1c-126">REST response</span></span>

<span data-ttu-id="44e1c-127">W przypadku powodzenia ta metoda zwraca obiekt **OrganizationProfile** w treści odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="44e1c-127">If successful, this method returns an **OrganizationProfile** object in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="44e1c-128">Kody powodzenia i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="44e1c-128">Response success and error codes</span></span>

<span data-ttu-id="44e1c-129">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie, oraz dodatkowe informacje o debugowaniu.</span><span class="sxs-lookup"><span data-stu-id="44e1c-129">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="44e1c-130">Użyj narzędzia śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="44e1c-130">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="44e1c-131">Aby uzyskać pełną listę, zobacz [Kody błędów](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="44e1c-131">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="44e1c-132">Przykład odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="44e1c-132">Response example</span></span>

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
