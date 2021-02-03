---
title: Aktualizowanie profilu biznesowego partnera
description: Jak zaktualizować profil biznesowy dla partnerów.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: parthpandyaMSFT
ms.author: parthp
ms.openlocfilehash: 6c61b51ab0680e36daa99c11dc8e8c3506259d29
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/19/2020
ms.locfileid: "97768274"
---
# <a name="update-the-partner-legal-business-profile"></a><span data-ttu-id="edabf-103">Aktualizowanie profilu biznesowego partnera</span><span class="sxs-lookup"><span data-stu-id="edabf-103">Update the partner legal business profile</span></span>

<span data-ttu-id="edabf-104">**Dotyczy**</span><span class="sxs-lookup"><span data-stu-id="edabf-104">**Applies To**</span></span>

- <span data-ttu-id="edabf-105">Centrum partnerskie</span><span class="sxs-lookup"><span data-stu-id="edabf-105">Partner Center</span></span>
- <span data-ttu-id="edabf-106">Centrum partnerskie obsługiwane przez firmę 21Vianet</span><span class="sxs-lookup"><span data-stu-id="edabf-106">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="edabf-107">Centrum partnerskie dla Microsoft Cloud Niemcy</span><span class="sxs-lookup"><span data-stu-id="edabf-107">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="edabf-108">Centrum partnerskie Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="edabf-108">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="edabf-109">Jak zaktualizować profil biznesowy dla partnerów.</span><span class="sxs-lookup"><span data-stu-id="edabf-109">How to update the partner legal business profile.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="edabf-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="edabf-110">Prerequisites</span></span>

- <span data-ttu-id="edabf-111">Poświadczenia zgodnie z opisem w temacie [uwierzytelnianie w centrum partnerskim](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="edabf-111">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="edabf-112">Ten scenariusz obsługuje tylko uwierzytelnianie przy użyciu aplikacji i poświadczeń użytkownika.</span><span class="sxs-lookup"><span data-stu-id="edabf-112">This scenario supports authentication with App+User credentials only.</span></span>

## <a name="c"></a><span data-ttu-id="edabf-113">C\#</span><span class="sxs-lookup"><span data-stu-id="edabf-113">C\#</span></span>

<span data-ttu-id="edabf-114">Aby zaktualizować profil biznesowy partnera, należy najpierw utworzyć wystąpienie obiektu **LegalBusinessProfile** i wypełnić go istniejącym profilem.</span><span class="sxs-lookup"><span data-stu-id="edabf-114">To update the partner legal business profile, first instantiate a **LegalBusinessProfile** object and populate it with the existing profile.</span></span> <span data-ttu-id="edabf-115">Aby uzyskać więcej informacji, zobacz sekcję [pobieranie służbowego profilu prawnego dla partnerów](get-legal-business-profile.md).</span><span class="sxs-lookup"><span data-stu-id="edabf-115">For more information, see [Get the partner legal business profile](get-legal-business-profile.md).</span></span> <span data-ttu-id="edabf-116">Następnie zaktualizuj właściwości, które należy zmienić.</span><span class="sxs-lookup"><span data-stu-id="edabf-116">Then, update the properties that you need to change.</span></span> <span data-ttu-id="edabf-117">Poniższy przykład kodu ilustruje zmianę adresu i podstawowych numerów telefonów kontaktów.</span><span class="sxs-lookup"><span data-stu-id="edabf-117">The following code example illustrates changing the address and primary contact phone numbers.</span></span>

<span data-ttu-id="edabf-118">Następnie Pobierz interfejs do kolekcji operacji profilu partnera z właściwości **IAggregatePartner. profile** .</span><span class="sxs-lookup"><span data-stu-id="edabf-118">Next, get an interface to the partner profile operations collection from the **IAggregatePartner.Profiles** property.</span></span> <span data-ttu-id="edabf-119">Następnie Pobierz wartość właściwości **LegalBusinessProfile** , aby uzyskać interfejs do operacji w profilu biznesowym.</span><span class="sxs-lookup"><span data-stu-id="edabf-119">Then, retrieve the value of the **LegalBusinessProfile** property to get an interface to legal business profile operations.</span></span> <span data-ttu-id="edabf-120">Na koniec Wywołaj metodę [**Update**](/dotnet/api/microsoft.store.partnercenter.profiles.ilegalbusinessprofile.update) lub [**UpdateAsync**](/dotnet/api/microsoft.store.partnercenter.profiles.ilegalbusinessprofile.updateasync) ze zmienionym obiektem w celu zaktualizowania profilu.</span><span class="sxs-lookup"><span data-stu-id="edabf-120">Finally, call the [**Update**](/dotnet/api/microsoft.store.partnercenter.profiles.ilegalbusinessprofile.update) or [**UpdateAsync**](/dotnet/api/microsoft.store.partnercenter.profiles.ilegalbusinessprofile.updateasync) method with the changed object to update the profile.</span></span>

``` csharp
// IAggregatePartner partnerOperations;

var legalBusinessProfile = partnerOperations.Profiles.LegalBusinessProfile.Get();

// Change the address and primary contact phone number.
legalBusinessProfile.Address.PhoneNumber = "4255550110";
legalBusinessProfile.PrimaryContact.PhoneNumber = "4255550110";

// Apply changes to the profile.
var updatedLegalBusinessProfile = partnerOperations.Profiles.LegalBusinessProfile.Update(legalBusinessProfile);
```

## <a name="rest-request"></a><span data-ttu-id="edabf-121">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="edabf-121">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="edabf-122">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="edabf-122">Request syntax</span></span>

| <span data-ttu-id="edabf-123">Metoda</span><span class="sxs-lookup"><span data-stu-id="edabf-123">Method</span></span>  | <span data-ttu-id="edabf-124">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="edabf-124">Request URI</span></span>                                                                    |
|---------|--------------------------------------------------------------------------------|
| <span data-ttu-id="edabf-125">**PUT**</span><span class="sxs-lookup"><span data-stu-id="edabf-125">**PUT**</span></span> | <span data-ttu-id="edabf-126">[*{baseURL}*](partner-center-rest-urls.md)/V1/Profiles/legalbusiness http/1.1</span><span class="sxs-lookup"><span data-stu-id="edabf-126">[*{baseURL}*](partner-center-rest-urls.md)/v1/profiles/legalbusiness HTTP/1.1</span></span> |

### <a name="request-headers"></a><span data-ttu-id="edabf-127">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="edabf-127">Request headers</span></span>

<span data-ttu-id="edabf-128">Aby uzyskać więcej informacji, zobacz [nagłówki REST Centrum partnerskiego](headers.md).</span><span class="sxs-lookup"><span data-stu-id="edabf-128">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="edabf-129">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="edabf-129">Request body</span></span>

<span data-ttu-id="edabf-130">Zasób profilu biznesowego firmy.</span><span class="sxs-lookup"><span data-stu-id="edabf-130">The legal business profile resource.</span></span>

### <a name="request-example"></a><span data-ttu-id="edabf-131">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="edabf-131">Request example</span></span>

```http
PUT https://api.partnercenter.microsoft.com/v1/profiles/legalbusiness HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 4549ac0c-0f1d-4d8f-b02f-6d36fadcccee
MS-CorrelationId: aa2a0d8c-7a41-470f-97ae-b82e6c338ee4
X-Locale: en-US
Content-Type: application/json
Host: api.partnercenter.microsoft.com
Content-Length: 806
Expect: 100-continue

{
    "CompanyName": "Lucerne Publishing",
    "Address": {
        "Country": "US",
        "Region": null,
        "City": "Redmond",
        "State": "WA",
        "AddressLine1": "123 Main Street",
        "AddressLine2": "",
        "PostalCode": "98052",
        "FirstName": "Gena",
        "LastName": "Soto",
        "PhoneNumber": "4255550110"
    },
    "PrimaryContact": {
        "FirstName": "Gena",
        "LastName": "Soto",
        "Email": "gena@lucernepublishing.com",
        "PhoneNumber": "4255550110"
    },
    "CompanyApproverAddress": {
        "Country": "US",
        "Region": null,
        "City": "Redmond",
        "State": "WA",
        "AddressLine1": "123 Main Street",
        "AddressLine2": "",
        "PostalCode": "98052",
        "FirstName": null,
        "LastName": null,
        "PhoneNumber": null
    },
    "CompanyApproverEmail": "gena@lucernepublishing.com",
    "VettingStatus": "authorized",
    "VettingSubStatus": "none",
    "Links": {
        "Self": {
            "Uri": "/profiles/legalbusiness",
            "Method": "GET",
            "Headers": []
        }
    },
    "Attributes": {
        "ObjectType": "LegalBusinessProfile"
    }
}
```

## <a name="rest-response"></a><span data-ttu-id="edabf-132">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="edabf-132">REST response</span></span>

<span data-ttu-id="edabf-133">Jeśli to się powiedzie, treść odpowiedzi zawiera zaktualizowane **LegalBusinessProfile**</span><span class="sxs-lookup"><span data-stu-id="edabf-133">If successful, the response body contains the updated **LegalBusinessProfile**</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="edabf-134">Kody sukcesu i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="edabf-134">Response success and error codes</span></span>

<span data-ttu-id="edabf-135">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie i dodatkowe informacje debugowania.</span><span class="sxs-lookup"><span data-stu-id="edabf-135">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="edabf-136">Użyj narzędzia do śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="edabf-136">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="edabf-137">Aby uzyskać pełną listę, zobacz [kody błędów Centrum partnerskiego](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="edabf-137">For the full list, see [Partner Center error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="edabf-138">Przykład odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="edabf-138">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 1157
Content-Type: application/json; charset=utf-8
MS-CorrelationId: aa2a0d8c-7a41-470f-97ae-b82e6c338ee4
MS-RequestId: 4549ac0c-0f1d-4d8f-b02f-6d36fadcccee
MS-CV: KZLU42qJ4EObO75q.0
MS-ServerId: 030020643
Date: Tue, 21 Mar 2017 22:03:15 GMT

{
    "companyName": "Lucerne Publishing",
    "address": {
        "country": "US",
        "city": "Redmond",
        "state": "WA",
        "addressLine1": "123 Main Street",
        "addressLine2": "",
        "postalCode": "98052",
        "firstName": "Gena",
        "lastName": "Soto",
        "phoneNumber": "4255550110"
    },
    "primaryContact": {
        "firstName": "Gena",
        "lastName": "Soto",
        "email": "gena@lucernepublishing.com",
        "phoneNumber": "4255550110"
    },
    "companyApproverAddress": {
        "country": "US",
        "city": "Redmond",
        "state": "WA",
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
