---
title: Aktualizowanie profilu pomocy technicznej
description: Aktualizuje profil obsługi użytkownika.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 605c509eeb18f301144fec6287c9611d5a5acfe2
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/19/2020
ms.locfileid: "97768270"
---
# <a name="update-support-profile"></a><span data-ttu-id="38dfd-103">Aktualizowanie profilu pomocy technicznej</span><span class="sxs-lookup"><span data-stu-id="38dfd-103">Update support profile</span></span>

<span data-ttu-id="38dfd-104">**Dotyczy**</span><span class="sxs-lookup"><span data-stu-id="38dfd-104">**Applies To**</span></span>

- <span data-ttu-id="38dfd-105">Centrum partnerskie</span><span class="sxs-lookup"><span data-stu-id="38dfd-105">Partner Center</span></span>
- <span data-ttu-id="38dfd-106">Centrum partnerskie obsługiwane przez firmę 21Vianet</span><span class="sxs-lookup"><span data-stu-id="38dfd-106">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="38dfd-107">Centrum partnerskie dla Microsoft Cloud Niemcy</span><span class="sxs-lookup"><span data-stu-id="38dfd-107">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="38dfd-108">Centrum partnerskie Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="38dfd-108">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="38dfd-109">Aktualizuje profil obsługi użytkownika.</span><span class="sxs-lookup"><span data-stu-id="38dfd-109">Updates a user's support profile.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="38dfd-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="38dfd-110">Prerequisites</span></span>

- <span data-ttu-id="38dfd-111">Poświadczenia zgodnie z opisem w temacie [uwierzytelnianie w centrum partnerskim](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="38dfd-111">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="38dfd-112">Ten scenariusz obsługuje tylko uwierzytelnianie przy użyciu aplikacji i poświadczeń użytkownika.</span><span class="sxs-lookup"><span data-stu-id="38dfd-112">This scenario supports authentication with App+User credentials only.</span></span>

## <a name="c"></a><span data-ttu-id="38dfd-113">C\#</span><span class="sxs-lookup"><span data-stu-id="38dfd-113">C\#</span></span>

<span data-ttu-id="38dfd-114">Aby zaktualizować profil pomocy technicznej, należy najpierw [uzyskać profil pomocy technicznej](get-support-profile.md) i wprowadzić wszelkie wprowadzone zmiany.</span><span class="sxs-lookup"><span data-stu-id="38dfd-114">To update your support profile, first [get your support profile](get-support-profile.md) and make any changes you wish.</span></span> <span data-ttu-id="38dfd-115">Następnie użyj swojej kolekcji [**IPartnerOperations. profile**](/dotnet/api/microsoft.store.partnercenter.ipartner.profiles) .</span><span class="sxs-lookup"><span data-stu-id="38dfd-115">Then, use your [**IPartnerOperations.Profiles**](/dotnet/api/microsoft.store.partnercenter.ipartner.profiles) collection.</span></span> <span data-ttu-id="38dfd-116">Wywołaj Właściwość [**SupportProfile**](/dotnet/api/microsoft.store.partnercenter.profiles.isupportprofile) , a następnie metodę [**Update ()**](/dotnet/api/microsoft.store.partnercenter.profiles.isupportprofile.update) lub [**UpdateAsync ()**](/dotnet/api/microsoft.store.partnercenter.profiles.isupportprofile.updateasync) .</span><span class="sxs-lookup"><span data-stu-id="38dfd-116">Call the [**SupportProfile**](/dotnet/api/microsoft.store.partnercenter.profiles.isupportprofile) property, followed by the [**Update()**](/dotnet/api/microsoft.store.partnercenter.profiles.isupportprofile.update) or [**UpdateAsync()**](/dotnet/api/microsoft.store.partnercenter.profiles.isupportprofile.updateasync) method.</span></span>

``` csharp
// IAggregatePartner partnerOperations;

// updated profile
SupportProfile newSupportProfile = new SupportProfile
{
   Email = supportProfile.Email,
   Website = supportProfile.Website,
   Telephone = new Random().Next(10000000, 99999999).ToString(CultureInfo.InvariantCulture)
};

SupportProfile updatedSupportProfile = partnerOperations.Profiles.SupportProfile.Update(newSupportProfile);
```

<span data-ttu-id="38dfd-117">**Przykład**: [aplikacja testowa konsoli](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="38dfd-117">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="38dfd-118">**Project**: PartnerCenterSDK. FeaturesSamples **Klasa**: UpdateSupportProfile.cs</span><span class="sxs-lookup"><span data-stu-id="38dfd-118">**Project**: PartnerCenterSDK.FeaturesSamples **Class**: UpdateSupportProfile.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="38dfd-119">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="38dfd-119">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="38dfd-120">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="38dfd-120">Request syntax</span></span>

| <span data-ttu-id="38dfd-121">Metoda</span><span class="sxs-lookup"><span data-stu-id="38dfd-121">Method</span></span>  | <span data-ttu-id="38dfd-122">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="38dfd-122">Request URI</span></span>                                                                     |
|---------|---------------------------------------------------------------------------------|
| <span data-ttu-id="38dfd-123">**PUT**</span><span class="sxs-lookup"><span data-stu-id="38dfd-123">**PUT**</span></span> | <span data-ttu-id="38dfd-124">[*{baseURL}*](partner-center-rest-urls.md)/V1/Profiles/supportprofile http/1.1</span><span class="sxs-lookup"><span data-stu-id="38dfd-124">[*{baseURL}*](partner-center-rest-urls.md)/v1/profiles/supportprofile HTTP/1.1</span></span> |

### <a name="request-headers"></a><span data-ttu-id="38dfd-125">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="38dfd-125">Request headers</span></span>

<span data-ttu-id="38dfd-126">Aby uzyskać więcej informacji, zobacz [nagłówki REST Centrum partnerskiego](headers.md).</span><span class="sxs-lookup"><span data-stu-id="38dfd-126">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="38dfd-127">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="38dfd-127">Request body</span></span>

<span data-ttu-id="38dfd-128">Zasób profilu pełnej obsługi.</span><span class="sxs-lookup"><span data-stu-id="38dfd-128">The full support profile resource.</span></span>

### <a name="request-example"></a><span data-ttu-id="38dfd-129">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="38dfd-129">Request example</span></span>

```http
PUT https://api.partnercenter.microsoft.com/v1/profiles/supportprofile HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 603f3cd9-01b8-48f2-b65d-855a246f5bfd
MS-CorrelationId: 20604323-50bf-4738-9968-c5486ab32be0
Content-Type: application/json
Content-Length: 167
Expect: 100-continue

{
    "Email": "email@sample.com",
    "Telephone": "4255555555",
    "Website": "www.microsoft.com",
    "ProfileType": "support_profile",
    "Attributes": {
        "ObjectType": "PartnerSupportProfile"
    }
}
```

## <a name="rest-response"></a><span data-ttu-id="38dfd-130">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="38dfd-130">REST response</span></span>

<span data-ttu-id="38dfd-131">Jeśli to się powiedzie, ta metoda zwraca zaktualizowane właściwości obiektu **SupportProfile** w treści odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="38dfd-131">If successful, this method returns updated **SupportProfile** object properties in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="38dfd-132">Kody sukcesu i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="38dfd-132">Response success and error codes</span></span>

<span data-ttu-id="38dfd-133">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie i dodatkowe informacje debugowania.</span><span class="sxs-lookup"><span data-stu-id="38dfd-133">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="38dfd-134">Użyj narzędzia do śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="38dfd-134">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="38dfd-135">Aby uzyskać pełną listę, zobacz [kody błędów](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="38dfd-135">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="38dfd-136">Przykład odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="38dfd-136">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 502
Content-Type: application/json
MS-CorrelationId: 20604323-50bf-4738-9968-c5486ab32be0
MS-RequestId: 603f3cd9-01b8-48f2-b65d-855a246f5bfd
Date: Wed, 25 Nov 2015 07:16:18 GMT

{
    "email": "email@sample.com",
    "telephone": "4255555555",
    "website": "www.microsoft.com",
    "profileType": "support_profile",
    "links": {
        "self": {
            "uri": "/v1/profiles/support",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "PartnerSupportProfile"
    }
}
```
