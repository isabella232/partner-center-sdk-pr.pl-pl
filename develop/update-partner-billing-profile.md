---
title: Aktualizowanie profilu rozliczeniowego partnera
description: Aktualizuje profil rozliczeniowy partnera.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: parthpandyaMSFT
ms.author: parthp
ms.openlocfilehash: 2b09a0045df15d774c892a59fba8502d4d4f7024
ms.sourcegitcommit: 4275f9f67f9479ce27af6a9fda96fe86d0bc0b44
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/05/2021
ms.locfileid: "111529770"
---
# <a name="update-the-partner-billing-profile"></a><span data-ttu-id="ef23d-103">Aktualizowanie profilu rozliczeniowego partnera</span><span class="sxs-lookup"><span data-stu-id="ef23d-103">Update the partner billing profile</span></span>

<span data-ttu-id="ef23d-104">**Dotyczy:** Partner Center | Partner Center obsługiwana przez firmę 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="ef23d-104">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="ef23d-105">Aktualizuje profil rozliczeniowy partnera</span><span class="sxs-lookup"><span data-stu-id="ef23d-105">Updates a partner's billing profile</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ef23d-106">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="ef23d-106">Prerequisites</span></span>

- <span data-ttu-id="ef23d-107">Poświadczenia zgodnie z opisem w te [Partner Center uwierzytelniania.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="ef23d-107">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="ef23d-108">Ten scenariusz obsługuje uwierzytelnianie tylko przy użyciu poświadczeń aplikacji i użytkownika.</span><span class="sxs-lookup"><span data-stu-id="ef23d-108">This scenario supports authentication with App+User credentials only.</span></span>

## <a name="c"></a><span data-ttu-id="ef23d-109">C\#</span><span class="sxs-lookup"><span data-stu-id="ef23d-109">C\#</span></span>

<span data-ttu-id="ef23d-110">Aby zaktualizować profil rozliczeniowy partnera, pobierz istniejący profil.</span><span class="sxs-lookup"><span data-stu-id="ef23d-110">To update a partner billing profile, retrieve the existing profile.</span></span> <span data-ttu-id="ef23d-111">Po zaktualizowaniu profilu użyj kolekcji **IAggregatePartner.Profiles** i wywołaj **właściwość BillingProfile.**</span><span class="sxs-lookup"><span data-stu-id="ef23d-111">Once you have updated the profile, use your **IAggregatePartner.Profiles** collection and call the **BillingProfile** property.</span></span> <span data-ttu-id="ef23d-112">Na koniec wywołaj **metodę Update().**</span><span class="sxs-lookup"><span data-stu-id="ef23d-112">Finally, call the **Update()** method.</span></span>

``` csharp
// IAggregatePartner partnerOperations;

BillingProfile existingBillingProfile = partnerOperations.Profiles.BillingProfile.Get();

// update the profile with a purchase order number
existingBillingProfile.PurchaseOrderNumber = new Random().Next(9000, 10000).ToString(CultureInfo.InvariantCulture);

BillingProfile updatedPartnerBillingProfile = partnerOperations.Profiles.BillingProfile.Update(existingBillingProfile);
```

<span data-ttu-id="ef23d-113">**Przykład:** [aplikacja testowa konsoli](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="ef23d-113">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="ef23d-114">**Project:** zestaw SDK Centrum partnerskiego Samples Class : UpdateBillingProfile.cs **(Klasa** przykładów zestaw SDK Centrum partnerskiego: UpdateBillingProfile.cs)</span><span class="sxs-lookup"><span data-stu-id="ef23d-114">**Project**: Partner Center SDK Samples **Class**: UpdateBillingProfile.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="ef23d-115">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="ef23d-115">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="ef23d-116">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="ef23d-116">Request syntax</span></span>

| <span data-ttu-id="ef23d-117">Metoda</span><span class="sxs-lookup"><span data-stu-id="ef23d-117">Method</span></span>  | <span data-ttu-id="ef23d-118">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="ef23d-118">Request URI</span></span>                                                              |
|---------|--------------------------------------------------------------------------|
| <span data-ttu-id="ef23d-119">**PUT**</span><span class="sxs-lookup"><span data-stu-id="ef23d-119">**PUT**</span></span> | <span data-ttu-id="ef23d-120">[*{baseURL}*](partner-center-rest-urls.md)/v1/profiles/billing HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="ef23d-120">[*{baseURL}*](partner-center-rest-urls.md)/v1/profiles/billing HTTP/1.1</span></span> |

### <a name="request-headers"></a><span data-ttu-id="ef23d-121">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="ef23d-121">Request headers</span></span>

<span data-ttu-id="ef23d-122">Aby uzyskać więcej informacji, [zobacz Partner Center REST headers (Nagłówki REST).](headers.md)</span><span class="sxs-lookup"><span data-stu-id="ef23d-122">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="ef23d-123">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="ef23d-123">Request body</span></span>

<span data-ttu-id="ef23d-124">Brak.</span><span class="sxs-lookup"><span data-stu-id="ef23d-124">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="ef23d-125">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="ef23d-125">Request example</span></span>

```http
PUT https://api.partnercenter.microsoft.com/v1/profiles/billing HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 9231559e-ed95-41e4-810b-e754ae32dc2f
MS-CorrelationId: cb9f3209-d020-4bf9-871c-e1f1c75348f8
Content-Length: 613
Expect: 100-continue

{
    "CompanyName":"TEST_TEST_BugBash1",
    "Address":{
        "Country":"US",
        "Region":null,
        "City":"Redmond",
        "State":"WA",
        "AddressLine1":"1 Microsoft Way",
        "AddressLine2":"","PostalCode":"98052",
        "FirstName":null,
        "LastName":null,
        "PhoneNumber":null
    },
    "PrimaryContact":{
        "FirstName":"Test",
        "LastName":"Customer",
        "Email":null,
        "PhoneNumber":""
    },
    "PurchaseOrderNumber":"9888",
    "TaxId":<TaxId>,
    "BillingCurrency":"USD",
    "Links":{
        "Self":{
            "Uri":"/profiles/billing",
            "Method":"GET","Headers":[]
        }
    },
    "Attributes":{
        "Etag":<etag>,
        "ObjectType":"BillingProfile"
    }
}
```

## <a name="rest-response"></a><span data-ttu-id="ef23d-126">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="ef23d-126">REST response</span></span>

<span data-ttu-id="ef23d-127">W przypadku powodzenia ta metoda zwraca obiekt **BillingProfile** w treści odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="ef23d-127">If successful, this method returns a **BillingProfile** object in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="ef23d-128">Kody powodzenia i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="ef23d-128">Response success and error codes</span></span>

<span data-ttu-id="ef23d-129">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie, oraz dodatkowe informacje o debugowaniu.</span><span class="sxs-lookup"><span data-stu-id="ef23d-129">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="ef23d-130">Użyj narzędzia śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="ef23d-130">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="ef23d-131">Aby uzyskać pełną listę, zobacz [Kody błędów](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="ef23d-131">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="ef23d-132">Przykład odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="ef23d-132">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 568
Content-Type: application/json; charset=utf-8
MS-CorrelationId: cb9f3209-d020-4bf9-871c-e1f1c75348f8
MS-RequestId: 9231559e-ed95-41e4-810b-e754ae32dc2f
Date: Mon, 21 Mar 2016 05:47:16 GMT

{
    "CompanyName":"TEST_TEST_BugBash1",
    "Address":{
        "Country":"US",
        "Region":null,
        "City":"Redmond",
        "State":"WA",
        "AddressLine1":"1 Microsoft Way",
        "AddressLine2":"","PostalCode":"98052",
        "FirstName":null,
        "LastName":null,
        "PhoneNumber":null
    },
    "PrimaryContact":{
        "FirstName":"Test",
        "LastName":"Customer",
        "Email":null,
        "PhoneNumber":""
    },
    "PurchaseOrderNumber":"9888",
    "TaxId":<TaxId>,
    "BillingCurrency":"USD",
    "Links":{
        "Self":{
            "Uri":"/profiles/billing",
            "Method":"GET","Headers":[]
        }
    },
    "Attributes":{
        "Etag":<etag>,
        "ObjectType":"BillingProfile"
    }
}
```
