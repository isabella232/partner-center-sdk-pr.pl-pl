---
title: Pobieranie profilu biznesowego partnera
description: Dowiedz się, jak uzyskać profil biznesowy dla celów prawnych przy użyciu interfejsów API.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: ba0654e364674bc2db129a0904d411c6fb67cbb9
ms.sourcegitcommit: b307fd75e305e0a88cfd1182cc01d2c9a108ce45
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/06/2021
ms.locfileid: "111549063"
---
# <a name="get-the-partner-legal-business-profile"></a><span data-ttu-id="4b036-103">Pobieranie profilu biznesowego partnera</span><span class="sxs-lookup"><span data-stu-id="4b036-103">Get the partner legal business profile</span></span>

<span data-ttu-id="4b036-104">**Dotyczy:** Partner Center | Partner Center obsługiwana przez firmę 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="4b036-104">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="4b036-105">Jak uzyskać legalny profil biznesowy partnera.</span><span class="sxs-lookup"><span data-stu-id="4b036-105">How to get a partner's legal business profile.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4b036-106">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="4b036-106">Prerequisites</span></span>

- <span data-ttu-id="4b036-107">Poświadczenia zgodnie z opisem w te [Partner Center uwierzytelniania.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="4b036-107">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="4b036-108">Ten scenariusz obsługuje uwierzytelnianie przy użyciu zarówno poświadczeń aplikacji autonomicznej, jak i aplikacji i użytkownika.</span><span class="sxs-lookup"><span data-stu-id="4b036-108">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

## <a name="c"></a><span data-ttu-id="4b036-109">C\#</span><span class="sxs-lookup"><span data-stu-id="4b036-109">C\#</span></span>

<span data-ttu-id="4b036-110">Aby uzyskać legalny profil biznesowy partnera, najpierw uzyskaj interfejs do kolekcji operacji profilu partnera z właściwości **IAggregatePartner.Profiles.**</span><span class="sxs-lookup"><span data-stu-id="4b036-110">To get the partner legal business profile, first get an interface to the collection of partner profile operations from the **IAggregatePartner.Profiles** property.</span></span> <span data-ttu-id="4b036-111">Następnie pobierz wartość właściwości **LegalBusinessProfile,** aby pobrać interfejs do operacji legalnych profilów biznesowych.</span><span class="sxs-lookup"><span data-stu-id="4b036-111">Then, get the value of the **LegalBusinessProfile** property to retrieve an interface to legal business profile operations.</span></span> <span data-ttu-id="4b036-112">Na koniec wywołaj [**metodę Get**](/dotnet/api/microsoft.store.partnercenter.profiles.ilegalbusinessprofile.get) lub [**GetAsync,**](/dotnet/api/microsoft.store.partnercenter.profiles.ilegalbusinessprofile.getasync) aby pobrać profil.</span><span class="sxs-lookup"><span data-stu-id="4b036-112">Finally, call the [**Get**](/dotnet/api/microsoft.store.partnercenter.profiles.ilegalbusinessprofile.get) or the [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.profiles.ilegalbusinessprofile.getasync) method to retrieve the profile.</span></span>

``` csharp
// IAggregatePartner partnerOperations;

var billingProfile = partnerOperations.Profiles.LegalBusinessProfile.Get();
```

<span data-ttu-id="4b036-113">**Przykład:** [aplikacja testowa konsoli](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="4b036-113">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="4b036-114">**Project:** zestaw SDK Centrum partnerskiego **Przykłady klasy:** GetLegalBusinessProfile.cs</span><span class="sxs-lookup"><span data-stu-id="4b036-114">**Project**: Partner Center SDK Samples **Class**: GetLegalBusinessProfile.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="4b036-115">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="4b036-115">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="4b036-116">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="4b036-116">Request syntax</span></span>

| <span data-ttu-id="4b036-117">Metoda</span><span class="sxs-lookup"><span data-stu-id="4b036-117">Method</span></span>  | <span data-ttu-id="4b036-118">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="4b036-118">Request URI</span></span>                                                                    |
|---------|--------------------------------------------------------------------------------|
| <span data-ttu-id="4b036-119">**Pobierz**</span><span class="sxs-lookup"><span data-stu-id="4b036-119">**GET**</span></span> | <span data-ttu-id="4b036-120">[*{baseURL}*](partner-center-rest-urls.md)/v1/profiles/legalbusiness HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="4b036-120">[*{baseURL}*](partner-center-rest-urls.md)/v1/profiles/legalbusiness HTTP/1.1</span></span> |

### <a name="request-headers"></a><span data-ttu-id="4b036-121">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="4b036-121">Request headers</span></span>

<span data-ttu-id="4b036-122">Aby uzyskać więcej informacji, [zobacz Partner Center REST headers (Nagłówki REST).](headers.md)</span><span class="sxs-lookup"><span data-stu-id="4b036-122">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="4b036-123">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="4b036-123">Request body</span></span>

<span data-ttu-id="4b036-124">Brak.</span><span class="sxs-lookup"><span data-stu-id="4b036-124">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="4b036-125">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="4b036-125">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="4b036-126">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="4b036-126">REST response</span></span>

<span data-ttu-id="4b036-127">W przypadku powodzenia ta metoda zwraca **obiekt LegalBusinessProfile** w treści odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="4b036-127">If successful, this method returns a **LegalBusinessProfile** object in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="4b036-128">Kody powodzenia i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="4b036-128">Response success and error codes</span></span>

<span data-ttu-id="4b036-129">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie, oraz dodatkowe informacje o debugowaniu.</span><span class="sxs-lookup"><span data-stu-id="4b036-129">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="4b036-130">Użyj narzędzia śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="4b036-130">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="4b036-131">Aby uzyskać pełną listę, zobacz [Partner Center kodów błędów REST.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="4b036-131">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="4b036-132">Przykład odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="4b036-132">Response example</span></span>

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
