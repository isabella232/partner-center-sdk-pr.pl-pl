---
title: Aktualizowanie profilu pomocy technicznej
description: Aktualizuje profil pomocy technicznej użytkownika.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 143328c5501f525d52911eead805d420f79b78ff
ms.sourcegitcommit: 4275f9f67f9479ce27af6a9fda96fe86d0bc0b44
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/05/2021
ms.locfileid: "111530348"
---
# <a name="update-support-profile"></a><span data-ttu-id="5daf7-103">Aktualizowanie profilu pomocy technicznej</span><span class="sxs-lookup"><span data-stu-id="5daf7-103">Update support profile</span></span>

<span data-ttu-id="5daf7-104">**Dotyczy:** Partner Center | Partner Center obsługiwana przez firmę 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="5daf7-104">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="5daf7-105">Aktualizuje profil pomocy technicznej użytkownika.</span><span class="sxs-lookup"><span data-stu-id="5daf7-105">Updates a user's support profile.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5daf7-106">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="5daf7-106">Prerequisites</span></span>

- <span data-ttu-id="5daf7-107">Poświadczenia zgodnie z opisem w te [Partner Center uwierzytelniania.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="5daf7-107">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="5daf7-108">Ten scenariusz obsługuje uwierzytelnianie tylko przy użyciu poświadczeń aplikacji i użytkownika.</span><span class="sxs-lookup"><span data-stu-id="5daf7-108">This scenario supports authentication with App+User credentials only.</span></span>

## <a name="c"></a><span data-ttu-id="5daf7-109">C\#</span><span class="sxs-lookup"><span data-stu-id="5daf7-109">C\#</span></span>

<span data-ttu-id="5daf7-110">Aby zaktualizować profil pomocy technicznej, najpierw [pobierz swój profil pomocy technicznej](get-support-profile.md) i wdaj wszelkie zmiany.</span><span class="sxs-lookup"><span data-stu-id="5daf7-110">To update your support profile, first [get your support profile](get-support-profile.md) and make any changes you wish.</span></span> <span data-ttu-id="5daf7-111">Następnie użyj [**kolekcji IPartnerOperations.Profiles.**](/dotnet/api/microsoft.store.partnercenter.ipartner.profiles)</span><span class="sxs-lookup"><span data-stu-id="5daf7-111">Then, use your [**IPartnerOperations.Profiles**](/dotnet/api/microsoft.store.partnercenter.ipartner.profiles) collection.</span></span> <span data-ttu-id="5daf7-112">Wywołaj [**właściwość SupportProfile,**](/dotnet/api/microsoft.store.partnercenter.profiles.isupportprofile) a następnie metodę [**Update()**](/dotnet/api/microsoft.store.partnercenter.profiles.isupportprofile.update) lub [**UpdateAsync().**](/dotnet/api/microsoft.store.partnercenter.profiles.isupportprofile.updateasync)</span><span class="sxs-lookup"><span data-stu-id="5daf7-112">Call the [**SupportProfile**](/dotnet/api/microsoft.store.partnercenter.profiles.isupportprofile) property, followed by the [**Update()**](/dotnet/api/microsoft.store.partnercenter.profiles.isupportprofile.update) or [**UpdateAsync()**](/dotnet/api/microsoft.store.partnercenter.profiles.isupportprofile.updateasync) method.</span></span>

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

<span data-ttu-id="5daf7-113">**Przykład:** [aplikacja testowa konsoli](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="5daf7-113">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="5daf7-114">**Project:** PartnerCenterSDK.FeaturesSamples, **klasa**: UpdateSupportProfile.cs</span><span class="sxs-lookup"><span data-stu-id="5daf7-114">**Project**: PartnerCenterSDK.FeaturesSamples **Class**: UpdateSupportProfile.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="5daf7-115">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="5daf7-115">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="5daf7-116">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="5daf7-116">Request syntax</span></span>

| <span data-ttu-id="5daf7-117">Metoda</span><span class="sxs-lookup"><span data-stu-id="5daf7-117">Method</span></span>  | <span data-ttu-id="5daf7-118">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="5daf7-118">Request URI</span></span>                                                                     |
|---------|---------------------------------------------------------------------------------|
| <span data-ttu-id="5daf7-119">**PUT**</span><span class="sxs-lookup"><span data-stu-id="5daf7-119">**PUT**</span></span> | <span data-ttu-id="5daf7-120">[*{baseURL}*](partner-center-rest-urls.md)/v1/profiles/supportprofile HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="5daf7-120">[*{baseURL}*](partner-center-rest-urls.md)/v1/profiles/supportprofile HTTP/1.1</span></span> |

### <a name="request-headers"></a><span data-ttu-id="5daf7-121">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="5daf7-121">Request headers</span></span>

<span data-ttu-id="5daf7-122">Aby uzyskać więcej informacji, [zobacz Partner Center REST headers (Nagłówki REST).](headers.md)</span><span class="sxs-lookup"><span data-stu-id="5daf7-122">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="5daf7-123">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="5daf7-123">Request body</span></span>

<span data-ttu-id="5daf7-124">Pełny zasób profilu pomocy technicznej.</span><span class="sxs-lookup"><span data-stu-id="5daf7-124">The full support profile resource.</span></span>

### <a name="request-example"></a><span data-ttu-id="5daf7-125">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="5daf7-125">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="5daf7-126">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="5daf7-126">REST response</span></span>

<span data-ttu-id="5daf7-127">W przypadku powodzenia ta metoda zwraca zaktualizowane **właściwości obiektu SupportProfile** w treści odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="5daf7-127">If successful, this method returns updated **SupportProfile** object properties in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="5daf7-128">Kody powodzenia i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="5daf7-128">Response success and error codes</span></span>

<span data-ttu-id="5daf7-129">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie, oraz dodatkowe informacje o debugowaniu.</span><span class="sxs-lookup"><span data-stu-id="5daf7-129">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="5daf7-130">Użyj narzędzia śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="5daf7-130">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="5daf7-131">Aby uzyskać pełną listę, zobacz [Kody błędów](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="5daf7-131">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="5daf7-132">Przykład odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="5daf7-132">Response example</span></span>

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
