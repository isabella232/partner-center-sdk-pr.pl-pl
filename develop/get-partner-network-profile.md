---
title: Pobieranie profilu Microsoft Partner Network
description: Pobiera obiekt reprezentujący profil MPN partnera.
ms.date: 09/17/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: f8f3e74462da05de0be47964beb34228650b1f53
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/19/2020
ms.locfileid: "97768482"
---
# <a name="get-microsoft-partner-network-profile"></a><span data-ttu-id="3832f-103">Pobieranie profilu Microsoft Partner Network</span><span class="sxs-lookup"><span data-stu-id="3832f-103">Get Microsoft Partner Network profile</span></span>

<span data-ttu-id="3832f-104">**Dotyczy**</span><span class="sxs-lookup"><span data-stu-id="3832f-104">**Applies To**</span></span>

- <span data-ttu-id="3832f-105">Centrum partnerskie</span><span class="sxs-lookup"><span data-stu-id="3832f-105">Partner Center</span></span>
- <span data-ttu-id="3832f-106">Centrum partnerskie obsługiwane przez firmę 21Vianet</span><span class="sxs-lookup"><span data-stu-id="3832f-106">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="3832f-107">Centrum partnerskie dla Microsoft Cloud Niemcy</span><span class="sxs-lookup"><span data-stu-id="3832f-107">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="3832f-108">Centrum partnerskie Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="3832f-108">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="3832f-109">Pobiera obiekt reprezentujący profil MPN partnera.</span><span class="sxs-lookup"><span data-stu-id="3832f-109">Gets an object representing the partner's MPN profile.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3832f-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="3832f-110">Prerequisites</span></span>

- <span data-ttu-id="3832f-111">Poświadczenia zgodnie z opisem w temacie [uwierzytelnianie w centrum partnerskim](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="3832f-111">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="3832f-112">Ten scenariusz obsługuje tylko uwierzytelnianie przy użyciu aplikacji i poświadczeń użytkownika.</span><span class="sxs-lookup"><span data-stu-id="3832f-112">This scenario supports authentication with App+User credentials only.</span></span>

## <a name="c"></a><span data-ttu-id="3832f-113">C\#</span><span class="sxs-lookup"><span data-stu-id="3832f-113">C\#</span></span>

<span data-ttu-id="3832f-114">Aby uzyskać profil sieci partnera, Użyj kolekcji **IAggregatePartner. profile** i Wywołaj Właściwość **MpnProfile** .</span><span class="sxs-lookup"><span data-stu-id="3832f-114">To get a partner network profile, use your **IAggregatePartner.Profiles** collection and call the **MpnProfile** property.</span></span> <span data-ttu-id="3832f-115">Na koniec wywołaj metody [**Get ()**](/dotnet/api/microsoft.store.partnercenter.profiles.impnprofile.get) lub [**GetAsync ()**](/dotnet/api/microsoft.store.partnercenter.profiles.impnprofile.getasync) .</span><span class="sxs-lookup"><span data-stu-id="3832f-115">Finally, call the [**Get()**](/dotnet/api/microsoft.store.partnercenter.profiles.impnprofile.get) or [**GetAsync()**](/dotnet/api/microsoft.store.partnercenter.profiles.impnprofile.getasync) methods.</span></span>

``` csharp
// IAggregatePartner partnerOperations;

var mpnProfile = partnerOperations.Profiles.MpnProfile.Get();
```

<span data-ttu-id="3832f-116">**Przykład**: [aplikacja testowa konsoli](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="3832f-116">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="3832f-117">**Project**:P Artnercentersdk. FeaturesSamples, **Klasa**: GetMPNProfile.cs</span><span class="sxs-lookup"><span data-stu-id="3832f-117">**Project**:PartnerCenterSDK.FeaturesSamples **Class**: GetMPNProfile.cs</span></span>

## <a name="java"></a><span data-ttu-id="3832f-118">Java</span><span class="sxs-lookup"><span data-stu-id="3832f-118">Java</span></span>

[!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

<span data-ttu-id="3832f-119">Aby uzyskać profil sieci partnera, użyj funkcji **IAggregatePartner. Getprofiles** i wywołaj funkcję **getMpnProfile** .</span><span class="sxs-lookup"><span data-stu-id="3832f-119">To get a partner network profile, use your **IAggregatePartner.getProfiles** function and call the **getMpnProfile** function.</span></span> <span data-ttu-id="3832f-120">Na koniec wywołaj funkcję **Get ()** .</span><span class="sxs-lookup"><span data-stu-id="3832f-120">Finally, call the **get()** function.</span></span>

```java
// IAggregatePartner partnerOperations;

MpnProfile mpnProfile = partnerOperations.getProfiles().getMpnProfile().get();
```

## <a name="powershell"></a><span data-ttu-id="3832f-121">PowerShell</span><span class="sxs-lookup"><span data-stu-id="3832f-121">PowerShell</span></span>

[!INCLUDE [Partner Center PowerShell module support details](../includes/powershell-module-support.md)]

<span data-ttu-id="3832f-122">Aby uzyskać profil sieci partnera, uruchom polecenie [**Get-PartnerMpnProfile**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerMpnProfile.md) .</span><span class="sxs-lookup"><span data-stu-id="3832f-122">To get a partner network profile, execute the [**Get-PartnerMpnProfile**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerMpnProfile.md) command.</span></span>

```powershell
Get-PartnerMpnProfile
```

## <a name="rest-request"></a><span data-ttu-id="3832f-123">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="3832f-123">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="3832f-124">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="3832f-124">Request syntax</span></span>

| <span data-ttu-id="3832f-125">Metoda</span><span class="sxs-lookup"><span data-stu-id="3832f-125">Method</span></span>  | <span data-ttu-id="3832f-126">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="3832f-126">Request URI</span></span>                                                          |
|---------|----------------------------------------------------------------------|
| <span data-ttu-id="3832f-127">**Pobierz**</span><span class="sxs-lookup"><span data-stu-id="3832f-127">**GET**</span></span> | <span data-ttu-id="3832f-128">[*{baseURL}*](partner-center-rest-urls.md)/V1/Profiles/MPN http/1.1</span><span class="sxs-lookup"><span data-stu-id="3832f-128">[*{baseURL}*](partner-center-rest-urls.md)/v1/profiles/mpn HTTP/1.1</span></span> |

### <a name="request-headers"></a><span data-ttu-id="3832f-129">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="3832f-129">Request headers</span></span>

<span data-ttu-id="3832f-130">Aby uzyskać więcej informacji, zobacz [nagłówki REST Centrum partnerskiego](headers.md).</span><span class="sxs-lookup"><span data-stu-id="3832f-130">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="3832f-131">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="3832f-131">Request body</span></span>

<span data-ttu-id="3832f-132">Brak.</span><span class="sxs-lookup"><span data-stu-id="3832f-132">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="3832f-133">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="3832f-133">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/profiles/mpn HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 76879323-92d1-437e-90dd-c84dbb9f7dec
MS-CorrelationId: cb9f3209-d020-4bf9-871c-e1f1c75348f8
Connection: Keep-Alive
```

## <a name="rest-response"></a><span data-ttu-id="3832f-134">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="3832f-134">REST response</span></span>

<span data-ttu-id="3832f-135">Jeśli to się powiedzie, metoda zwraca obiekt **MPNProfile** w treści odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="3832f-135">If successful, this method returns a **MPNProfile** object in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="3832f-136">Kody sukcesu i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="3832f-136">Response success and error codes</span></span>

<span data-ttu-id="3832f-137">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie i dodatkowe informacje debugowania.</span><span class="sxs-lookup"><span data-stu-id="3832f-137">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="3832f-138">Użyj narzędzia do śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="3832f-138">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="3832f-139">Aby uzyskać pełną listę, zobacz [kody błędów](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="3832f-139">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="3832f-140">Przykład odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="3832f-140">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 177
Content-Type: application/json; charset=utf-8
MS-CorrelationId: cb9f3209-d020-4bf9-871c-e1f1c75348f8
MS-RequestId: 76879323-92d1-437e-90dd-c84dbb9f7dec
Date: Mon, 21 Mar 2016 05:51:29 GMT

{
    "mpnId":"<mpnID>",
    "profileType":"MpnProfile",
    "links":{
        "self":{
            "uri":"/profiles/mpn",
            "method":"GET",
            "headers":[]
        }
    },
    "attributes":{
        "objectType":"MpnProfile"
    }
}
```
