---
title: Pobieranie profilu Microsoft Partner Network
description: Pobiera obiekt reprezentujący profil MPN partnera.
ms.date: 09/17/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 38c12a9a9755b9838b7742d9f38c5cbd52b81210
ms.sourcegitcommit: b307fd75e305e0a88cfd1182cc01d2c9a108ce45
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/06/2021
ms.locfileid: "111548859"
---
# <a name="get-microsoft-partner-network-profile"></a><span data-ttu-id="e67ba-103">Pobieranie profilu Microsoft Partner Network</span><span class="sxs-lookup"><span data-stu-id="e67ba-103">Get Microsoft Partner Network profile</span></span>

<span data-ttu-id="e67ba-104">**Dotyczy:** Partner Center | Partner Center obsługiwana przez firmę 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="e67ba-104">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="e67ba-105">Pobiera obiekt reprezentujący profil MPN partnera.</span><span class="sxs-lookup"><span data-stu-id="e67ba-105">Gets an object representing the partner's MPN profile.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e67ba-106">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="e67ba-106">Prerequisites</span></span>

- <span data-ttu-id="e67ba-107">Poświadczenia zgodnie z opisem w [te Partner Center uwierzytelniania.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="e67ba-107">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="e67ba-108">Ten scenariusz obsługuje uwierzytelnianie tylko przy użyciu poświadczeń aplikacji i użytkownika.</span><span class="sxs-lookup"><span data-stu-id="e67ba-108">This scenario supports authentication with App+User credentials only.</span></span>

## <a name="c"></a><span data-ttu-id="e67ba-109">C\#</span><span class="sxs-lookup"><span data-stu-id="e67ba-109">C\#</span></span>

<span data-ttu-id="e67ba-110">Aby uzyskać profil sieci partnera, użyj **kolekcji IAggregatePartner.Profiles** i wywołaj **właściwość MpnProfile.**</span><span class="sxs-lookup"><span data-stu-id="e67ba-110">To get a partner network profile, use your **IAggregatePartner.Profiles** collection and call the **MpnProfile** property.</span></span> <span data-ttu-id="e67ba-111">Na koniec wywołaj [**metody Get()**](/dotnet/api/microsoft.store.partnercenter.profiles.impnprofile.get) [**lub GetAsync().**](/dotnet/api/microsoft.store.partnercenter.profiles.impnprofile.getasync)</span><span class="sxs-lookup"><span data-stu-id="e67ba-111">Finally, call the [**Get()**](/dotnet/api/microsoft.store.partnercenter.profiles.impnprofile.get) or [**GetAsync()**](/dotnet/api/microsoft.store.partnercenter.profiles.impnprofile.getasync) methods.</span></span>

``` csharp
// IAggregatePartner partnerOperations;

var mpnProfile = partnerOperations.Profiles.MpnProfile.Get();
```

<span data-ttu-id="e67ba-112">**Przykład:** [aplikacja testowa konsoli](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="e67ba-112">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="e67ba-113">**Project**:P artnerCenterSDK.FeaturesKlasa : GetMPNProfile.cs</span><span class="sxs-lookup"><span data-stu-id="e67ba-113">**Project**:PartnerCenterSDK.FeaturesSamples **Class**: GetMPNProfile.cs</span></span>

## <a name="java"></a><span data-ttu-id="e67ba-114">Java</span><span class="sxs-lookup"><span data-stu-id="e67ba-114">Java</span></span>

[!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

<span data-ttu-id="e67ba-115">Aby uzyskać profil sieci partnera, użyj funkcji **IAggregatePartner.getProfiles** i wywołaj funkcję **getMpnProfile.**</span><span class="sxs-lookup"><span data-stu-id="e67ba-115">To get a partner network profile, use your **IAggregatePartner.getProfiles** function and call the **getMpnProfile** function.</span></span> <span data-ttu-id="e67ba-116">Na koniec wywołaj **funkcję get().**</span><span class="sxs-lookup"><span data-stu-id="e67ba-116">Finally, call the **get()** function.</span></span>

```java
// IAggregatePartner partnerOperations;

MpnProfile mpnProfile = partnerOperations.getProfiles().getMpnProfile().get();
```

## <a name="powershell"></a><span data-ttu-id="e67ba-117">PowerShell</span><span class="sxs-lookup"><span data-stu-id="e67ba-117">PowerShell</span></span>

[!INCLUDE [Partner Center PowerShell module support details](../includes/powershell-module-support.md)]

<span data-ttu-id="e67ba-118">Aby uzyskać profil sieci partnera, wykonaj polecenie [**Get-PartnerMpnProfile.**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerMpnProfile.md)</span><span class="sxs-lookup"><span data-stu-id="e67ba-118">To get a partner network profile, execute the [**Get-PartnerMpnProfile**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerMpnProfile.md) command.</span></span>

```powershell
Get-PartnerMpnProfile
```

## <a name="rest-request"></a><span data-ttu-id="e67ba-119">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="e67ba-119">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="e67ba-120">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="e67ba-120">Request syntax</span></span>

| <span data-ttu-id="e67ba-121">Metoda</span><span class="sxs-lookup"><span data-stu-id="e67ba-121">Method</span></span>  | <span data-ttu-id="e67ba-122">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="e67ba-122">Request URI</span></span>                                                          |
|---------|----------------------------------------------------------------------|
| <span data-ttu-id="e67ba-123">**Pobierz**</span><span class="sxs-lookup"><span data-stu-id="e67ba-123">**GET**</span></span> | <span data-ttu-id="e67ba-124">[*{baseURL}*](partner-center-rest-urls.md)/v1/profiles/mpn HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="e67ba-124">[*{baseURL}*](partner-center-rest-urls.md)/v1/profiles/mpn HTTP/1.1</span></span> |

### <a name="request-headers"></a><span data-ttu-id="e67ba-125">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="e67ba-125">Request headers</span></span>

<span data-ttu-id="e67ba-126">Aby uzyskać więcej informacji, [zobacz Partner Center REST headers (Nagłówki REST).](headers.md)</span><span class="sxs-lookup"><span data-stu-id="e67ba-126">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="e67ba-127">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="e67ba-127">Request body</span></span>

<span data-ttu-id="e67ba-128">Brak.</span><span class="sxs-lookup"><span data-stu-id="e67ba-128">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="e67ba-129">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="e67ba-129">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/profiles/mpn HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 76879323-92d1-437e-90dd-c84dbb9f7dec
MS-CorrelationId: cb9f3209-d020-4bf9-871c-e1f1c75348f8
Connection: Keep-Alive
```

## <a name="rest-response"></a><span data-ttu-id="e67ba-130">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="e67ba-130">REST response</span></span>

<span data-ttu-id="e67ba-131">Jeśli to się powiedzie, ta metoda zwraca obiekt **MPNProfile** w treści odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="e67ba-131">If successful, this method returns a **MPNProfile** object in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="e67ba-132">Kody powodzenia i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="e67ba-132">Response success and error codes</span></span>

<span data-ttu-id="e67ba-133">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie, oraz dodatkowe informacje o debugowaniu.</span><span class="sxs-lookup"><span data-stu-id="e67ba-133">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="e67ba-134">Użyj narzędzia śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="e67ba-134">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="e67ba-135">Aby uzyskać pełną listę, zobacz [Kody błędów](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="e67ba-135">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="e67ba-136">Przykład odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="e67ba-136">Response example</span></span>

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
