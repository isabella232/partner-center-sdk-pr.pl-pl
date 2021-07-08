---
title: Pobieranie profilu rozliczeniowego partnera
description: Pobiera obiekt reprezentujący profil rozliczeniowy partnera.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 225d8ea2d92933838ae47eaf3308276aa1f1684c
ms.sourcegitcommit: b307fd75e305e0a88cfd1182cc01d2c9a108ce45
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/06/2021
ms.locfileid: "111548978"
---
# <a name="get-partner-billing-profile"></a><span data-ttu-id="f81af-103">Pobieranie profilu rozliczeniowego partnera</span><span class="sxs-lookup"><span data-stu-id="f81af-103">Get partner billing profile</span></span>

<span data-ttu-id="f81af-104">**Dotyczy:** Partner Center | Partner Center obsługiwana przez firmę 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="f81af-104">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="f81af-105">Pobiera obiekt reprezentujący profil rozliczeniowy partnera.</span><span class="sxs-lookup"><span data-stu-id="f81af-105">Gets an object representing the partner's billing profile.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f81af-106">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="f81af-106">Prerequisites</span></span>

- <span data-ttu-id="f81af-107">Poświadczenia zgodnie z opisem w te [Partner Center uwierzytelniania.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="f81af-107">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="f81af-108">Ten scenariusz obsługuje uwierzytelnianie tylko przy użyciu poświadczeń aplikacji i użytkownika.</span><span class="sxs-lookup"><span data-stu-id="f81af-108">This scenario supports authentication with App+User credentials only.</span></span>

## <a name="c"></a><span data-ttu-id="f81af-109">C\#</span><span class="sxs-lookup"><span data-stu-id="f81af-109">C\#</span></span>

<span data-ttu-id="f81af-110">Aby uzyskać profil rozliczeniowy partnera, użyj **kolekcji IAggregatePartner.Profiles** i wywołaj **właściwość BillingProfile.**</span><span class="sxs-lookup"><span data-stu-id="f81af-110">To get a partner billing profile, use your **IAggregatePartner.Profiles** collection and call the **BillingProfile** property.</span></span> <span data-ttu-id="f81af-111">Na koniec wywołaj [**metody Get()**](/dotnet/api/microsoft.store.partnercenter.profiles.ibillingprofile.get) [**lub GetAsync().**](/dotnet/api/microsoft.store.partnercenter.profiles.ibillingprofile.getasync)</span><span class="sxs-lookup"><span data-stu-id="f81af-111">Finally, call the [**Get()**](/dotnet/api/microsoft.store.partnercenter.profiles.ibillingprofile.get) or [**GetAsync()**](/dotnet/api/microsoft.store.partnercenter.profiles.ibillingprofile.getasync) methods.</span></span>

``` csharp
// IAggregatePartner partnerOperations;

BillingProfile billingProfile = partnerOperations.Profiles.BillingProfile.Get();
```

<span data-ttu-id="f81af-112">**Przykład:** [aplikacja testowa konsoli](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="f81af-112">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="f81af-113">**Project:** PartnerCenterSDK.FeaturesSamples, **klasa**: GetBillingProfile.cs</span><span class="sxs-lookup"><span data-stu-id="f81af-113">**Project**: PartnerCenterSDK.FeaturesSamples **Class**: GetBillingProfile.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="f81af-114">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="f81af-114">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="f81af-115">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="f81af-115">Request syntax</span></span>

| <span data-ttu-id="f81af-116">Metoda</span><span class="sxs-lookup"><span data-stu-id="f81af-116">Method</span></span>  | <span data-ttu-id="f81af-117">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="f81af-117">Request URI</span></span>                                                              |
|---------|--------------------------------------------------------------------------|
| <span data-ttu-id="f81af-118">**Pobierz**</span><span class="sxs-lookup"><span data-stu-id="f81af-118">**GET**</span></span> | <span data-ttu-id="f81af-119">[*{baseURL}*](partner-center-rest-urls.md)/v1/profiles/billing HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="f81af-119">[*{baseURL}*](partner-center-rest-urls.md)/v1/profiles/billing HTTP/1.1</span></span> |

### <a name="request-headers"></a><span data-ttu-id="f81af-120">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="f81af-120">Request headers</span></span>

<span data-ttu-id="f81af-121">Aby uzyskać więcej informacji, [zobacz Partner Center REST headers (Nagłówki REST).](headers.md)</span><span class="sxs-lookup"><span data-stu-id="f81af-121">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="f81af-122">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="f81af-122">Request body</span></span>

<span data-ttu-id="f81af-123">Brak.</span><span class="sxs-lookup"><span data-stu-id="f81af-123">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="f81af-124">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="f81af-124">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/profiles/billing HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: a0dd6cde-b24c-413c-af24-416446dc5599
MS-CorrelationId: 1bb03149-88d2-4bc2-9cc1-d6e83890fa9e
```

## <a name="rest-response"></a><span data-ttu-id="f81af-125">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="f81af-125">REST response</span></span>

<span data-ttu-id="f81af-126">W przypadku powodzenia ta metoda zwraca obiekt **BillingProfile** w treści odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="f81af-126">If successful, this method returns a **BillingProfile** object in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="f81af-127">Kody powodzenia i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="f81af-127">Response success and error codes</span></span>

<span data-ttu-id="f81af-128">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie, oraz dodatkowe informacje o debugowaniu.</span><span class="sxs-lookup"><span data-stu-id="f81af-128">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="f81af-129">Użyj narzędzia śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="f81af-129">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="f81af-130">Aby uzyskać pełną listę, zobacz [Kody błędów](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="f81af-130">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="f81af-131">Przykład odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="f81af-131">Response example</span></span>

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
