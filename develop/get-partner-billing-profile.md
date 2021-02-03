---
title: Pobieranie profilu rozliczeniowego partnera
description: Pobiera obiekt reprezentujący profil rozliczania partnera.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 94c5ff8fc351282ca3b4721511f02ba6a0cc403c
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/19/2020
ms.locfileid: "97768434"
---
# <a name="get-partner-billing-profile"></a><span data-ttu-id="e506c-103">Pobieranie profilu rozliczeniowego partnera</span><span class="sxs-lookup"><span data-stu-id="e506c-103">Get partner billing profile</span></span>

<span data-ttu-id="e506c-104">**Dotyczy**</span><span class="sxs-lookup"><span data-stu-id="e506c-104">**Applies To**</span></span>

- <span data-ttu-id="e506c-105">Centrum partnerskie</span><span class="sxs-lookup"><span data-stu-id="e506c-105">Partner Center</span></span>
- <span data-ttu-id="e506c-106">Centrum partnerskie obsługiwane przez firmę 21Vianet</span><span class="sxs-lookup"><span data-stu-id="e506c-106">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="e506c-107">Centrum partnerskie dla Microsoft Cloud Niemcy</span><span class="sxs-lookup"><span data-stu-id="e506c-107">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="e506c-108">Centrum partnerskie Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="e506c-108">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="e506c-109">Pobiera obiekt reprezentujący profil rozliczania partnera.</span><span class="sxs-lookup"><span data-stu-id="e506c-109">Gets an object representing the partner's billing profile.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e506c-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="e506c-110">Prerequisites</span></span>

- <span data-ttu-id="e506c-111">Poświadczenia zgodnie z opisem w temacie [uwierzytelnianie w centrum partnerskim](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="e506c-111">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="e506c-112">Ten scenariusz obsługuje tylko uwierzytelnianie przy użyciu aplikacji i poświadczeń użytkownika.</span><span class="sxs-lookup"><span data-stu-id="e506c-112">This scenario supports authentication with App+User credentials only.</span></span>

## <a name="c"></a><span data-ttu-id="e506c-113">C\#</span><span class="sxs-lookup"><span data-stu-id="e506c-113">C\#</span></span>

<span data-ttu-id="e506c-114">Aby uzyskać profil rozliczania partnera, Użyj kolekcji **IAggregatePartner. profile** i Wywołaj Właściwość **BillingProfile** .</span><span class="sxs-lookup"><span data-stu-id="e506c-114">To get a partner billing profile, use your **IAggregatePartner.Profiles** collection and call the **BillingProfile** property.</span></span> <span data-ttu-id="e506c-115">Na koniec wywołaj metody [**Get ()**](/dotnet/api/microsoft.store.partnercenter.profiles.ibillingprofile.get) lub [**GetAsync ()**](/dotnet/api/microsoft.store.partnercenter.profiles.ibillingprofile.getasync) .</span><span class="sxs-lookup"><span data-stu-id="e506c-115">Finally, call the [**Get()**](/dotnet/api/microsoft.store.partnercenter.profiles.ibillingprofile.get) or [**GetAsync()**](/dotnet/api/microsoft.store.partnercenter.profiles.ibillingprofile.getasync) methods.</span></span>

``` csharp
// IAggregatePartner partnerOperations;

BillingProfile billingProfile = partnerOperations.Profiles.BillingProfile.Get();
```

<span data-ttu-id="e506c-116">**Przykład**: [aplikacja testowa konsoli](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="e506c-116">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="e506c-117">**Project**: PartnerCenterSDK. FeaturesSamples **Klasa**: GetBillingProfile.cs</span><span class="sxs-lookup"><span data-stu-id="e506c-117">**Project**: PartnerCenterSDK.FeaturesSamples **Class**: GetBillingProfile.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="e506c-118">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="e506c-118">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="e506c-119">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="e506c-119">Request syntax</span></span>

| <span data-ttu-id="e506c-120">Metoda</span><span class="sxs-lookup"><span data-stu-id="e506c-120">Method</span></span>  | <span data-ttu-id="e506c-121">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="e506c-121">Request URI</span></span>                                                              |
|---------|--------------------------------------------------------------------------|
| <span data-ttu-id="e506c-122">**Pobierz**</span><span class="sxs-lookup"><span data-stu-id="e506c-122">**GET**</span></span> | <span data-ttu-id="e506c-123">[*{baseURL}*](partner-center-rest-urls.md)/V1/Profiles/Billing http/1.1</span><span class="sxs-lookup"><span data-stu-id="e506c-123">[*{baseURL}*](partner-center-rest-urls.md)/v1/profiles/billing HTTP/1.1</span></span> |

### <a name="request-headers"></a><span data-ttu-id="e506c-124">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="e506c-124">Request headers</span></span>

<span data-ttu-id="e506c-125">Aby uzyskać więcej informacji, zobacz [nagłówki REST Centrum partnerskiego](headers.md).</span><span class="sxs-lookup"><span data-stu-id="e506c-125">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="e506c-126">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="e506c-126">Request body</span></span>

<span data-ttu-id="e506c-127">Brak.</span><span class="sxs-lookup"><span data-stu-id="e506c-127">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="e506c-128">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="e506c-128">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/profiles/billing HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: a0dd6cde-b24c-413c-af24-416446dc5599
MS-CorrelationId: 1bb03149-88d2-4bc2-9cc1-d6e83890fa9e
```

## <a name="rest-response"></a><span data-ttu-id="e506c-129">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="e506c-129">REST response</span></span>

<span data-ttu-id="e506c-130">Jeśli to się powiedzie, metoda zwraca obiekt **BillingProfile** w treści odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="e506c-130">If successful, this method returns a **BillingProfile** object in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="e506c-131">Kody sukcesu i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="e506c-131">Response success and error codes</span></span>

<span data-ttu-id="e506c-132">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie i dodatkowe informacje debugowania.</span><span class="sxs-lookup"><span data-stu-id="e506c-132">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="e506c-133">Użyj narzędzia do śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="e506c-133">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="e506c-134">Aby uzyskać pełną listę, zobacz [kody błędów](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="e506c-134">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="e506c-135">Przykład odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="e506c-135">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 568
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 1bb03149-88d2-4bc2-9cc1-d6e83890fa9e
MS-RequestId: a0dd6cde-b24c-413c-af24-416446dc5599
Date: Tue, 22 Mar 2016 17:10:02 GMT

{
    "companyName":"TEST_TEST_BugBash1",
    "address":{
        "country":"US",
        "city":"Redmond",
        "state":"WA",
        "addressLine1":"1 Microsoft Way",
        "addressLine2":"","postalCode":"98052"
    },
    "primaryContact":{
        "firstName":"James",
        "lastName":"Burk",
        "phoneNumber":"2066017143"
    },
    "purchaseOrderNumber":"9888",
    "taxId":"12-345678",
    "billingCurrency":"USD",
    "profileType":"BillingProfile",
    "links":{
        "self":{
            "uri":"/profiles/billing",
            "method":"GET",
            "headers":[]
        }
    },
    "attributes":{
        "etag":<etag>,
        "objectType":"BillingProfile"
    }
}
```
