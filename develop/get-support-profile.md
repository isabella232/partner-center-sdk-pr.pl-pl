---
title: Pobieranie profilu pomocy technicznej
description: Pobiera obiekt reprezentujący profil pomocy technicznej użytkownika.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: b112ccbbff731795c21f95845a08be9e9dfb6775
ms.sourcegitcommit: b307fd75e305e0a88cfd1182cc01d2c9a108ce45
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/06/2021
ms.locfileid: "111548638"
---
# <a name="get-support-profile"></a><span data-ttu-id="21a4a-103">Pobieranie profilu pomocy technicznej</span><span class="sxs-lookup"><span data-stu-id="21a4a-103">Get support profile</span></span>

<span data-ttu-id="21a4a-104">**Dotyczy:** Partner Center | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="21a4a-104">**Applies to**: Partner Center | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="21a4a-105">Pobiera obiekt reprezentujący profil pomocy technicznej użytkownika.</span><span class="sxs-lookup"><span data-stu-id="21a4a-105">Gets an object representing a user's support profile.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="21a4a-106">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="21a4a-106">Prerequisites</span></span>

- <span data-ttu-id="21a4a-107">Poświadczenia zgodnie z opisem w [te Partner Center uwierzytelniania.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="21a4a-107">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="21a4a-108">Ten scenariusz obsługuje uwierzytelnianie tylko przy użyciu poświadczeń aplikacji i użytkownika.</span><span class="sxs-lookup"><span data-stu-id="21a4a-108">This scenario supports authentication with App+User credentials only.</span></span>

## <a name="c"></a><span data-ttu-id="21a4a-109">C\#</span><span class="sxs-lookup"><span data-stu-id="21a4a-109">C\#</span></span>

<span data-ttu-id="21a4a-110">Aby uzyskać profil pomocy technicznej, użyj **kolekcji IAggregatePartner.Profiles.**</span><span class="sxs-lookup"><span data-stu-id="21a4a-110">To get your support profile, use your **IAggregatePartner.Profiles** collection.</span></span> <span data-ttu-id="21a4a-111">Wywołaj [**właściwość SupportProfile,**](/dotnet/api/microsoft.store.partnercenter.profiles.isupportprofile) a następnie metody [**Get()**](/dotnet/api/microsoft.store.partnercenter.profiles.isupportprofile.get) lub [**GetAsync().**](/dotnet/api/microsoft.store.partnercenter.profiles.isupportprofile.getasync)</span><span class="sxs-lookup"><span data-stu-id="21a4a-111">Call the [**SupportProfile**](/dotnet/api/microsoft.store.partnercenter.profiles.isupportprofile) property, followed by the [**Get()**](/dotnet/api/microsoft.store.partnercenter.profiles.isupportprofile.get) or [**GetAsync()**](/dotnet/api/microsoft.store.partnercenter.profiles.isupportprofile.getasync) methods.</span></span>

``` csharp
// IAggregatePartner partnerOperations;

SupportProfile supportProfile = partnerOperations.Profiles.SupportProfile.Get();
```

<span data-ttu-id="21a4a-112">**Przykład:** [aplikacja testowa konsoli](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="21a4a-112">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="21a4a-113">**Project:** PartnerCenterSDK.FeaturesKlasa Samples: GetSupportProfile.cs </span><span class="sxs-lookup"><span data-stu-id="21a4a-113">**Project**: PartnerCenterSDK.FeaturesSamples **Class**: GetSupportProfile.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="21a4a-114">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="21a4a-114">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="21a4a-115">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="21a4a-115">Request syntax</span></span>

| <span data-ttu-id="21a4a-116">Metoda</span><span class="sxs-lookup"><span data-stu-id="21a4a-116">Method</span></span>  | <span data-ttu-id="21a4a-117">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="21a4a-117">Request URI</span></span>                                                              |
|---------|--------------------------------------------------------------------------|
| <span data-ttu-id="21a4a-118">**Pobierz**</span><span class="sxs-lookup"><span data-stu-id="21a4a-118">**GET**</span></span> | <span data-ttu-id="21a4a-119">[*{baseURL}*](partner-center-rest-urls.md)/v1/profiles/support HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="21a4a-119">[*{baseURL}*](partner-center-rest-urls.md)/v1/profiles/support HTTP/1.1</span></span> |

### <a name="request-headers"></a><span data-ttu-id="21a4a-120">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="21a4a-120">Request headers</span></span>

<span data-ttu-id="21a4a-121">Aby uzyskać więcej informacji, [zobacz Partner Center REST headers (Nagłówki REST).](headers.md)</span><span class="sxs-lookup"><span data-stu-id="21a4a-121">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="21a4a-122">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="21a4a-122">Request body</span></span>

<span data-ttu-id="21a4a-123">Brak.</span><span class="sxs-lookup"><span data-stu-id="21a4a-123">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="21a4a-124">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="21a4a-124">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/profiles/support HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 07029132-385d-416f-a9a6-df5e9e4c78d3
MS-CorrelationId: 20604323-50bf-4738-9968-c5486ab32be0
```

## <a name="rest-response"></a><span data-ttu-id="21a4a-125">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="21a4a-125">REST response</span></span>

<span data-ttu-id="21a4a-126">W przypadku powodzenia ta metoda zwraca obiekt **SupportProfile** w treści odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="21a4a-126">If successful, this method returns a **SupportProfile** object in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="21a4a-127">Kody powodzenia i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="21a4a-127">Response success and error codes</span></span>

<span data-ttu-id="21a4a-128">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie, oraz dodatkowe informacje o debugowaniu.</span><span class="sxs-lookup"><span data-stu-id="21a4a-128">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="21a4a-129">Użyj narzędzia śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="21a4a-129">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="21a4a-130">Aby uzyskać pełną listę, zobacz [Kody błędów](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="21a4a-130">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="21a4a-131">Przykład odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="21a4a-131">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 502
Content-Type: application/json
MS-CorrelationId: 20604323-50bf-4738-9968-c5486ab32be0
MS-RequestId: 07029132-385d-416f-a9a6-df5e9e4c78d3
Date: Wed, 25 Nov 2015 07:16:17 GMT

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
