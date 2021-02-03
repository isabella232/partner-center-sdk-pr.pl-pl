---
title: Pobieranie profilu pomocy technicznej
description: Pobiera obiekt reprezentujący profil obsługi użytkownika.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: b8b0fa533aaba74418985ea02cbb13bd722cede2
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/19/2020
ms.locfileid: "97768413"
---
# <a name="get-support-profile"></a><span data-ttu-id="7c083-103">Pobieranie profilu pomocy technicznej</span><span class="sxs-lookup"><span data-stu-id="7c083-103">Get support profile</span></span>

<span data-ttu-id="7c083-104">**Dotyczy**</span><span class="sxs-lookup"><span data-stu-id="7c083-104">**Applies To**</span></span>

- <span data-ttu-id="7c083-105">Centrum partnerskie</span><span class="sxs-lookup"><span data-stu-id="7c083-105">Partner Center</span></span>
- <span data-ttu-id="7c083-106">Centrum partnerskie dla Microsoft Cloud Niemcy</span><span class="sxs-lookup"><span data-stu-id="7c083-106">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="7c083-107">Centrum partnerskie Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="7c083-107">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="7c083-108">Pobiera obiekt reprezentujący profil obsługi użytkownika.</span><span class="sxs-lookup"><span data-stu-id="7c083-108">Gets an object representing a user's support profile.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7c083-109">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="7c083-109">Prerequisites</span></span>

- <span data-ttu-id="7c083-110">Poświadczenia zgodnie z opisem w temacie [uwierzytelnianie w centrum partnerskim](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="7c083-110">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="7c083-111">Ten scenariusz obsługuje tylko uwierzytelnianie przy użyciu aplikacji i poświadczeń użytkownika.</span><span class="sxs-lookup"><span data-stu-id="7c083-111">This scenario supports authentication with App+User credentials only.</span></span>

## <a name="c"></a><span data-ttu-id="7c083-112">C\#</span><span class="sxs-lookup"><span data-stu-id="7c083-112">C\#</span></span>

<span data-ttu-id="7c083-113">Aby uzyskać profil pomocy technicznej, Użyj kolekcji **IAggregatePartner. profile** .</span><span class="sxs-lookup"><span data-stu-id="7c083-113">To get your support profile, use your **IAggregatePartner.Profiles** collection.</span></span> <span data-ttu-id="7c083-114">Wywołaj Właściwość [**SupportProfile**](/dotnet/api/microsoft.store.partnercenter.profiles.isupportprofile) , a następnie metodę [**Get ()**](/dotnet/api/microsoft.store.partnercenter.profiles.isupportprofile.get) lub [**GetAsync ()**](/dotnet/api/microsoft.store.partnercenter.profiles.isupportprofile.getasync) .</span><span class="sxs-lookup"><span data-stu-id="7c083-114">Call the [**SupportProfile**](/dotnet/api/microsoft.store.partnercenter.profiles.isupportprofile) property, followed by the [**Get()**](/dotnet/api/microsoft.store.partnercenter.profiles.isupportprofile.get) or [**GetAsync()**](/dotnet/api/microsoft.store.partnercenter.profiles.isupportprofile.getasync) methods.</span></span>

``` csharp
// IAggregatePartner partnerOperations;

SupportProfile supportProfile = partnerOperations.Profiles.SupportProfile.Get();
```

<span data-ttu-id="7c083-115">**Przykład**: [aplikacja testowa konsoli](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="7c083-115">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="7c083-116">**Project**: PartnerCenterSDK. FeaturesSamples **Klasa**: GetSupportProfile.cs</span><span class="sxs-lookup"><span data-stu-id="7c083-116">**Project**: PartnerCenterSDK.FeaturesSamples **Class**: GetSupportProfile.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="7c083-117">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="7c083-117">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="7c083-118">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="7c083-118">Request syntax</span></span>

| <span data-ttu-id="7c083-119">Metoda</span><span class="sxs-lookup"><span data-stu-id="7c083-119">Method</span></span>  | <span data-ttu-id="7c083-120">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="7c083-120">Request URI</span></span>                                                              |
|---------|--------------------------------------------------------------------------|
| <span data-ttu-id="7c083-121">**Pobierz**</span><span class="sxs-lookup"><span data-stu-id="7c083-121">**GET**</span></span> | <span data-ttu-id="7c083-122">[*{baseURL}*](partner-center-rest-urls.md)/V1/Profiles/support http/1.1</span><span class="sxs-lookup"><span data-stu-id="7c083-122">[*{baseURL}*](partner-center-rest-urls.md)/v1/profiles/support HTTP/1.1</span></span> |

### <a name="request-headers"></a><span data-ttu-id="7c083-123">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="7c083-123">Request headers</span></span>

<span data-ttu-id="7c083-124">Aby uzyskać więcej informacji, zobacz [nagłówki REST Centrum partnerskiego](headers.md).</span><span class="sxs-lookup"><span data-stu-id="7c083-124">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="7c083-125">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="7c083-125">Request body</span></span>

<span data-ttu-id="7c083-126">Brak.</span><span class="sxs-lookup"><span data-stu-id="7c083-126">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="7c083-127">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="7c083-127">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/profiles/support HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 07029132-385d-416f-a9a6-df5e9e4c78d3
MS-CorrelationId: 20604323-50bf-4738-9968-c5486ab32be0
```

## <a name="rest-response"></a><span data-ttu-id="7c083-128">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="7c083-128">REST response</span></span>

<span data-ttu-id="7c083-129">Jeśli to się powiedzie, metoda zwraca obiekt **SupportProfile** w treści odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="7c083-129">If successful, this method returns a **SupportProfile** object in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="7c083-130">Kody sukcesu i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="7c083-130">Response success and error codes</span></span>

<span data-ttu-id="7c083-131">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie i dodatkowe informacje debugowania.</span><span class="sxs-lookup"><span data-stu-id="7c083-131">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="7c083-132">Użyj narzędzia do śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="7c083-132">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="7c083-133">Aby uzyskać pełną listę, zobacz [kody błędów](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="7c083-133">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="7c083-134">Przykład odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="7c083-134">Response example</span></span>

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
