---
title: Aktualizowanie profilu rozliczeniowego partnera
description: Aktualizuje profil rozliczeń partnera.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: parthpandyaMSFT
ms.author: parthp
ms.openlocfilehash: 34e7d2396d6dbdd45a6cf87a3bda481f51326f1e
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/08/2020
ms.locfileid: "97768002"
---
# <a name="update-the-partner-billing-profile"></a><span data-ttu-id="9add6-103">Aktualizowanie profilu rozliczeniowego partnera</span><span class="sxs-lookup"><span data-stu-id="9add6-103">Update the partner billing profile</span></span>

<span data-ttu-id="9add6-104">**Dotyczy**</span><span class="sxs-lookup"><span data-stu-id="9add6-104">**Applies To**</span></span>

- <span data-ttu-id="9add6-105">Centrum partnerskie</span><span class="sxs-lookup"><span data-stu-id="9add6-105">Partner Center</span></span>
- <span data-ttu-id="9add6-106">Centrum partnerskie obsługiwane przez firmę 21Vianet</span><span class="sxs-lookup"><span data-stu-id="9add6-106">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="9add6-107">Centrum partnerskie dla Microsoft Cloud Niemcy</span><span class="sxs-lookup"><span data-stu-id="9add6-107">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="9add6-108">Centrum partnerskie Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="9add6-108">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="9add6-109">Aktualizuje profil rozliczeń partnera</span><span class="sxs-lookup"><span data-stu-id="9add6-109">Updates a partner's billing profile</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9add6-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="9add6-110">Prerequisites</span></span>

- <span data-ttu-id="9add6-111">Poświadczenia zgodnie z opisem w temacie [uwierzytelnianie w centrum partnerskim](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="9add6-111">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="9add6-112">Ten scenariusz obsługuje tylko uwierzytelnianie przy użyciu aplikacji i poświadczeń użytkownika.</span><span class="sxs-lookup"><span data-stu-id="9add6-112">This scenario supports authentication with App+User credentials only.</span></span>

## <a name="c"></a><span data-ttu-id="9add6-113">C\#</span><span class="sxs-lookup"><span data-stu-id="9add6-113">C\#</span></span>

<span data-ttu-id="9add6-114">Aby zaktualizować profil rozliczania partnera, Pobierz istniejący profil.</span><span class="sxs-lookup"><span data-stu-id="9add6-114">To update a partner billing profile, retrieve the existing profile.</span></span> <span data-ttu-id="9add6-115">Po zaktualizowaniu profilu Użyj kolekcji **IAggregatePartner. profile** i Wywołaj Właściwość **BillingProfile** .</span><span class="sxs-lookup"><span data-stu-id="9add6-115">Once you have updated the profile, use your **IAggregatePartner.Profiles** collection and call the **BillingProfile** property.</span></span> <span data-ttu-id="9add6-116">Na koniec Wywołaj metodę **Update ()** .</span><span class="sxs-lookup"><span data-stu-id="9add6-116">Finally, call the **Update()** method.</span></span>

``` csharp
// IAggregatePartner partnerOperations;

BillingProfile existingBillingProfile = partnerOperations.Profiles.BillingProfile.Get();

// update the profile with a purchase order number
existingBillingProfile.PurchaseOrderNumber = new Random().Next(9000, 10000).ToString(CultureInfo.InvariantCulture);

BillingProfile updatedPartnerBillingProfile = partnerOperations.Profiles.BillingProfile.Update(existingBillingProfile);
```

<span data-ttu-id="9add6-117">**Przykład**: [aplikacja testowa konsoli](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="9add6-117">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="9add6-118">**Projekt**: **Klasa** przykładów zestawu SDK centrum partnerskiego: UpdateBillingProfile.cs</span><span class="sxs-lookup"><span data-stu-id="9add6-118">**Project**: Partner Center SDK Samples **Class**: UpdateBillingProfile.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="9add6-119">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="9add6-119">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="9add6-120">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="9add6-120">Request syntax</span></span>

| <span data-ttu-id="9add6-121">Metoda</span><span class="sxs-lookup"><span data-stu-id="9add6-121">Method</span></span>  | <span data-ttu-id="9add6-122">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="9add6-122">Request URI</span></span>                                                              |
|---------|--------------------------------------------------------------------------|
| <span data-ttu-id="9add6-123">**PUT**</span><span class="sxs-lookup"><span data-stu-id="9add6-123">**PUT**</span></span> | <span data-ttu-id="9add6-124">[*{baseURL}*](partner-center-rest-urls.md)/V1/Profiles/Billing http/1.1</span><span class="sxs-lookup"><span data-stu-id="9add6-124">[*{baseURL}*](partner-center-rest-urls.md)/v1/profiles/billing HTTP/1.1</span></span> |

### <a name="request-headers"></a><span data-ttu-id="9add6-125">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="9add6-125">Request headers</span></span>

<span data-ttu-id="9add6-126">Aby uzyskać więcej informacji, zobacz [nagłówki REST Centrum partnerskiego](headers.md).</span><span class="sxs-lookup"><span data-stu-id="9add6-126">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="9add6-127">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="9add6-127">Request body</span></span>

<span data-ttu-id="9add6-128">Brak.</span><span class="sxs-lookup"><span data-stu-id="9add6-128">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="9add6-129">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="9add6-129">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="9add6-130">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="9add6-130">REST response</span></span>

<span data-ttu-id="9add6-131">Jeśli to się powiedzie, metoda zwraca obiekt **BillingProfile** w treści odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="9add6-131">If successful, this method returns a **BillingProfile** object in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="9add6-132">Kody sukcesu i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="9add6-132">Response success and error codes</span></span>

<span data-ttu-id="9add6-133">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie i dodatkowe informacje debugowania.</span><span class="sxs-lookup"><span data-stu-id="9add6-133">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="9add6-134">Użyj narzędzia do śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="9add6-134">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="9add6-135">Aby uzyskać pełną listę, zobacz [kody błędów](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="9add6-135">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="9add6-136">Przykład odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="9add6-136">Response example</span></span>

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
