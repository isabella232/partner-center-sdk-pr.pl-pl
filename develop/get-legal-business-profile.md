---
title: Pobieranie profilu biznesowego partnera
description: Jak uzyskać legalny profil biznesowy partnera.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 5d7055dd0a6586e16b078109db4252250561eb29
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/19/2020
ms.locfileid: "97768438"
---
# <a name="get-the-partner-legal-business-profile"></a><span data-ttu-id="d86cb-103">Pobieranie profilu biznesowego partnera</span><span class="sxs-lookup"><span data-stu-id="d86cb-103">Get the partner legal business profile</span></span>

<span data-ttu-id="d86cb-104">**Dotyczy**</span><span class="sxs-lookup"><span data-stu-id="d86cb-104">**Applies To**</span></span>

- <span data-ttu-id="d86cb-105">Centrum partnerskie</span><span class="sxs-lookup"><span data-stu-id="d86cb-105">Partner Center</span></span>
- <span data-ttu-id="d86cb-106">Centrum partnerskie obsługiwane przez firmę 21Vianet</span><span class="sxs-lookup"><span data-stu-id="d86cb-106">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="d86cb-107">Centrum partnerskie dla Microsoft Cloud Niemcy</span><span class="sxs-lookup"><span data-stu-id="d86cb-107">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="d86cb-108">Centrum partnerskie Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="d86cb-108">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="d86cb-109">Jak uzyskać legalny profil biznesowy partnera.</span><span class="sxs-lookup"><span data-stu-id="d86cb-109">How to get a partner's legal business profile.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d86cb-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="d86cb-110">Prerequisites</span></span>

- <span data-ttu-id="d86cb-111">Poświadczenia zgodnie z opisem w temacie [uwierzytelnianie w centrum partnerskim](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="d86cb-111">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="d86cb-112">Ten scenariusz obsługuje uwierzytelnianie zarówno w przypadku aplikacji autonomicznych, jak i aplikacji oraz poświadczeń użytkownika.</span><span class="sxs-lookup"><span data-stu-id="d86cb-112">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

## <a name="c"></a><span data-ttu-id="d86cb-113">C\#</span><span class="sxs-lookup"><span data-stu-id="d86cb-113">C\#</span></span>

<span data-ttu-id="d86cb-114">Aby uzyskać legalny profil biznesowy partnera, najpierw Uzyskaj interfejs do kolekcji operacji profilu partnera z właściwości **IAggregatePartner. profile** .</span><span class="sxs-lookup"><span data-stu-id="d86cb-114">To get the partner legal business profile, first get an interface to the collection of partner profile operations from the **IAggregatePartner.Profiles** property.</span></span> <span data-ttu-id="d86cb-115">Następnie Pobierz wartość właściwości **LegalBusinessProfile** , aby pobrać interfejs do firmowych operacji profilowania.</span><span class="sxs-lookup"><span data-stu-id="d86cb-115">Then, get the value of the **LegalBusinessProfile** property to retrieve an interface to legal business profile operations.</span></span> <span data-ttu-id="d86cb-116">Na koniec Wywołaj metodę [**Get**](/dotnet/api/microsoft.store.partnercenter.profiles.ilegalbusinessprofile.get) lub [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.profiles.ilegalbusinessprofile.getasync) , aby pobrać profil.</span><span class="sxs-lookup"><span data-stu-id="d86cb-116">Finally, call the [**Get**](/dotnet/api/microsoft.store.partnercenter.profiles.ilegalbusinessprofile.get) or the [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.profiles.ilegalbusinessprofile.getasync) method to retrieve the profile.</span></span>

``` csharp
// IAggregatePartner partnerOperations;

var billingProfile = partnerOperations.Profiles.LegalBusinessProfile.Get();
```

<span data-ttu-id="d86cb-117">**Przykład**: [aplikacja testowa konsoli](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="d86cb-117">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="d86cb-118">**Projekt**: **Klasa** przykładów zestawu SDK centrum partnerskiego: GetLegalBusinessProfile.cs</span><span class="sxs-lookup"><span data-stu-id="d86cb-118">**Project**: Partner Center SDK Samples **Class**: GetLegalBusinessProfile.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="d86cb-119">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="d86cb-119">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="d86cb-120">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="d86cb-120">Request syntax</span></span>

| <span data-ttu-id="d86cb-121">Metoda</span><span class="sxs-lookup"><span data-stu-id="d86cb-121">Method</span></span>  | <span data-ttu-id="d86cb-122">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="d86cb-122">Request URI</span></span>                                                                    |
|---------|--------------------------------------------------------------------------------|
| <span data-ttu-id="d86cb-123">**Pobierz**</span><span class="sxs-lookup"><span data-stu-id="d86cb-123">**GET**</span></span> | <span data-ttu-id="d86cb-124">[*{baseURL}*](partner-center-rest-urls.md)/V1/Profiles/legalbusiness http/1.1</span><span class="sxs-lookup"><span data-stu-id="d86cb-124">[*{baseURL}*](partner-center-rest-urls.md)/v1/profiles/legalbusiness HTTP/1.1</span></span> |

### <a name="request-headers"></a><span data-ttu-id="d86cb-125">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="d86cb-125">Request headers</span></span>

<span data-ttu-id="d86cb-126">Aby uzyskać więcej informacji, zobacz [nagłówki REST Centrum partnerskiego](headers.md).</span><span class="sxs-lookup"><span data-stu-id="d86cb-126">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="d86cb-127">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="d86cb-127">Request body</span></span>

<span data-ttu-id="d86cb-128">Brak.</span><span class="sxs-lookup"><span data-stu-id="d86cb-128">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="d86cb-129">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="d86cb-129">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/profiles/legalbusiness?vettingVersion=Current HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 7391249f-cba0-467c-b026-7b3a60196422
MS-CorrelationId: 98a091a0-67db-4eeb-ae0d-7e8b2e39c1d2
X-Locale: en-US
Host: api.partnercenter.microsoft.com
Connection: Keep-Alive
```

## <a name="rest-response"></a><span data-ttu-id="d86cb-130">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="d86cb-130">REST response</span></span>

<span data-ttu-id="d86cb-131">Jeśli to się powiedzie, metoda zwraca obiekt **LegalBusinessProfile** w treści odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="d86cb-131">If successful, this method returns a **LegalBusinessProfile** object in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="d86cb-132">Kody sukcesu i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="d86cb-132">Response success and error codes</span></span>

<span data-ttu-id="d86cb-133">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie i dodatkowe informacje debugowania.</span><span class="sxs-lookup"><span data-stu-id="d86cb-133">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="d86cb-134">Użyj narzędzia do śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="d86cb-134">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="d86cb-135">Aby uzyskać pełną listę, zobacz [kody błędów REST centrum partnera](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="d86cb-135">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="d86cb-136">Przykład odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="d86cb-136">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 1151
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 98a091a0-67db-4eeb-ae0d-7e8b2e39c1d2
MS-RequestId: 7391249f-cba0-467c-b026-7b3a60196422
MS-CV: MEgCpJUoGUeXG+4a.0
MS-ServerId: 030011719
Date: Tue, 21 Mar 2017 17:29:52 GMT

{
    "companyName": "Lucerne Publishing",
    "address": {
        "country": "US",
        "city": "Buffalo",
        "state": "NY",
        "addressLine1": "123 Main Street",
        "addressLine2": "",
        "postalCode": "98052",
        "firstName": "Gena",
        "lastName": "Soto",
        "phoneNumber": "4255550100"
    },
    "primaryContact": {
        "firstName": "Gena",
        "lastName": "Soto",
        "email": "gena@lucernepublishing.com",
        "phoneNumber": "4255550100"
    },
    "companyApproverAddress": {
        "country": "US",
        "city": "Buffalo",
        "state": "NY",
        "addressLine1": "123 Main Street",
        "addressLine2": "",
        "postalCode": "98052"
    },
    "companyApproverEmail": "gena@lucernepublishing.com",
    "vettingStatus": "authorized",
    "vettingSubStatus": "none",
    "profileType": "LegalBusinessProfile",
    "links": {
        "self": {
            "uri": "/profiles/legalbusiness",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "LegalBusinessProfile"
    }
}
```
