---
title: Aktualizowanie profilu biznesowego partnera
description: Jak zaktualizować profil biznesowy partnera.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: parthpandyaMSFT
ms.author: parthp
ms.openlocfilehash: cb9f5815e0019c5e9b648dfd865e9752f0afdf05
ms.sourcegitcommit: 4275f9f67f9479ce27af6a9fda96fe86d0bc0b44
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/05/2021
ms.locfileid: "111530331"
---
# <a name="update-the-partner-legal-business-profile"></a><span data-ttu-id="c7e61-103">Aktualizowanie profilu biznesowego partnera</span><span class="sxs-lookup"><span data-stu-id="c7e61-103">Update the partner legal business profile</span></span>

<span data-ttu-id="c7e61-104">**Dotyczy:** Partner Center | Partner Center obsługiwana przez firmę 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="c7e61-104">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="c7e61-105">Jak zaktualizować profil biznesowy partnera.</span><span class="sxs-lookup"><span data-stu-id="c7e61-105">How to update the partner legal business profile.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c7e61-106">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="c7e61-106">Prerequisites</span></span>

- <span data-ttu-id="c7e61-107">Poświadczenia zgodnie z opisem w te [Partner Center uwierzytelniania.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="c7e61-107">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="c7e61-108">Ten scenariusz obsługuje uwierzytelnianie tylko przy użyciu poświadczeń aplikacji i użytkownika.</span><span class="sxs-lookup"><span data-stu-id="c7e61-108">This scenario supports authentication with App+User credentials only.</span></span>

## <a name="c"></a><span data-ttu-id="c7e61-109">C\#</span><span class="sxs-lookup"><span data-stu-id="c7e61-109">C\#</span></span>

<span data-ttu-id="c7e61-110">Aby zaktualizować legalny profil biznesowy partnera, najpierw należy utworzyć jego wystąpienia w obiekcie **LegalBusinessProfile** i wypełnić go istniejącym profilem.</span><span class="sxs-lookup"><span data-stu-id="c7e61-110">To update the partner legal business profile, first instantiate a **LegalBusinessProfile** object and populate it with the existing profile.</span></span> <span data-ttu-id="c7e61-111">Aby uzyskać więcej informacji, zobacz Get the partner legal business profile (Uzyskiwanie [profilu biznesowego partnera).](get-legal-business-profile.md)</span><span class="sxs-lookup"><span data-stu-id="c7e61-111">For more information, see [Get the partner legal business profile](get-legal-business-profile.md).</span></span> <span data-ttu-id="c7e61-112">Następnie zaktualizuj właściwości, które należy zmienić.</span><span class="sxs-lookup"><span data-stu-id="c7e61-112">Then, update the properties that you need to change.</span></span> <span data-ttu-id="c7e61-113">Poniższy przykład kodu ilustruje zmianę adresu i podstawowych numerów telefonów kontaktów.</span><span class="sxs-lookup"><span data-stu-id="c7e61-113">The following code example illustrates changing the address and primary contact phone numbers.</span></span>

<span data-ttu-id="c7e61-114">Następnie pobierz interfejs do kolekcji operacji profilu partnera z właściwości **IAggregatePartner.Profiles.**</span><span class="sxs-lookup"><span data-stu-id="c7e61-114">Next, get an interface to the partner profile operations collection from the **IAggregatePartner.Profiles** property.</span></span> <span data-ttu-id="c7e61-115">Następnie pobierz wartość właściwości **LegalBusinessProfile,** aby uzyskać interfejs do operacji legalnych profilów biznesowych.</span><span class="sxs-lookup"><span data-stu-id="c7e61-115">Then, retrieve the value of the **LegalBusinessProfile** property to get an interface to legal business profile operations.</span></span> <span data-ttu-id="c7e61-116">Na koniec wywołaj [**metodę Update**](/dotnet/api/microsoft.store.partnercenter.profiles.ilegalbusinessprofile.update) lub [**UpdateAsync**](/dotnet/api/microsoft.store.partnercenter.profiles.ilegalbusinessprofile.updateasync) ze zmienionym obiektem, aby zaktualizować profil.</span><span class="sxs-lookup"><span data-stu-id="c7e61-116">Finally, call the [**Update**](/dotnet/api/microsoft.store.partnercenter.profiles.ilegalbusinessprofile.update) or [**UpdateAsync**](/dotnet/api/microsoft.store.partnercenter.profiles.ilegalbusinessprofile.updateasync) method with the changed object to update the profile.</span></span>

``` csharp
// IAggregatePartner partnerOperations;

var legalBusinessProfile = partnerOperations.Profiles.LegalBusinessProfile.Get();

// Change the address and primary contact phone number.
legalBusinessProfile.Address.PhoneNumber = "4255550110";
legalBusinessProfile.PrimaryContact.PhoneNumber = "4255550110";

// Apply changes to the profile.
var updatedLegalBusinessProfile = partnerOperations.Profiles.LegalBusinessProfile.Update(legalBusinessProfile);
```

## <a name="rest-request"></a><span data-ttu-id="c7e61-117">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="c7e61-117">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="c7e61-118">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="c7e61-118">Request syntax</span></span>

| <span data-ttu-id="c7e61-119">Metoda</span><span class="sxs-lookup"><span data-stu-id="c7e61-119">Method</span></span>  | <span data-ttu-id="c7e61-120">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="c7e61-120">Request URI</span></span>                                                                    |
|---------|--------------------------------------------------------------------------------|
| <span data-ttu-id="c7e61-121">**PUT**</span><span class="sxs-lookup"><span data-stu-id="c7e61-121">**PUT**</span></span> | <span data-ttu-id="c7e61-122">[*{baseURL}*](partner-center-rest-urls.md)/v1/profiles/legalbusiness HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="c7e61-122">[*{baseURL}*](partner-center-rest-urls.md)/v1/profiles/legalbusiness HTTP/1.1</span></span> |

### <a name="request-headers"></a><span data-ttu-id="c7e61-123">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="c7e61-123">Request headers</span></span>

<span data-ttu-id="c7e61-124">Aby uzyskać więcej informacji, [zobacz Partner Center REST headers (Nagłówki REST).](headers.md)</span><span class="sxs-lookup"><span data-stu-id="c7e61-124">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="c7e61-125">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="c7e61-125">Request body</span></span>

<span data-ttu-id="c7e61-126">Zasób legalnych profilów biznesowych.</span><span class="sxs-lookup"><span data-stu-id="c7e61-126">The legal business profile resource.</span></span>

### <a name="request-example"></a><span data-ttu-id="c7e61-127">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="c7e61-127">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="c7e61-128">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="c7e61-128">REST response</span></span>

<span data-ttu-id="c7e61-129">W przypadku powodzenia treść odpowiedzi zawiera zaktualizowany **plik LegalBusinessProfile**</span><span class="sxs-lookup"><span data-stu-id="c7e61-129">If successful, the response body contains the updated **LegalBusinessProfile**</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="c7e61-130">Kody powodzenia i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="c7e61-130">Response success and error codes</span></span>

<span data-ttu-id="c7e61-131">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie, oraz dodatkowe informacje o debugowaniu.</span><span class="sxs-lookup"><span data-stu-id="c7e61-131">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="c7e61-132">Użyj narzędzia śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="c7e61-132">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="c7e61-133">Aby uzyskać pełną listę, zobacz [Partner Center kodów błędów](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="c7e61-133">For the full list, see [Partner Center error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="c7e61-134">Przykład odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="c7e61-134">Response example</span></span>

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
