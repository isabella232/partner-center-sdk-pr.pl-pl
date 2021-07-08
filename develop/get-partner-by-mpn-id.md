---
title: Weryfikowanie identyfikatora MPN partnera
description: Dowiedz się, jak zweryfikować identyfikator Microsoft Partner Network partnera (identyfikator MPN), żądając profilu MPN partnera za pośrednictwem języka C lub interfejsu \# API REST Partner Center.
ms.date: 09/29/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 6bd51850c7bc5a099a34f9c028a58e247c2600a3
ms.sourcegitcommit: b307fd75e305e0a88cfd1182cc01d2c9a108ce45
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/06/2021
ms.locfileid: "111548825"
---
# <a name="verify-a-partner-mpn-id-via-c-or-the-partner-center-rest-api"></a><span data-ttu-id="9e65e-103">Weryfikowanie identyfikatora MPN partnera za pośrednictwem języka C \# lub interfejsu API REST Partner Center API</span><span class="sxs-lookup"><span data-stu-id="9e65e-103">Verify a partner MPN ID via C\# or the Partner Center REST API</span></span>

<span data-ttu-id="9e65e-104">**Dotyczy:** Partner Center | Partner Center obsługiwana przez firmę 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="9e65e-104">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="9e65e-105">Jak zweryfikować identyfikator Microsoft Partner Network partnera (IDENTYFIKATOR MPN).</span><span class="sxs-lookup"><span data-stu-id="9e65e-105">How to verify a partner's Microsoft Partner Network identifier (MPN ID).</span></span>

<span data-ttu-id="9e65e-106">Technika pokazana w tym miejscu weryfikuje identyfikator Microsoft Partner Network partnera, żądając profilu MPN partnera z Centrum partnerskiego.</span><span class="sxs-lookup"><span data-stu-id="9e65e-106">The technique shown here verifies the partner's Microsoft Partner Network identifier by requesting the partner's MPN profile from partner center.</span></span> <span data-ttu-id="9e65e-107">Identyfikator jest uznawany za prawidłowy, jeśli żądanie zakończy się pomyślnie.</span><span class="sxs-lookup"><span data-stu-id="9e65e-107">The identifier is considered valid if the request succeeds.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9e65e-108">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="9e65e-108">Prerequisites</span></span>

- <span data-ttu-id="9e65e-109">Poświadczenia zgodnie z opisem w [te Partner Center uwierzytelniania.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="9e65e-109">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="9e65e-110">Ten scenariusz obsługuje uwierzytelnianie tylko przy użyciu poświadczeń aplikacji i użytkownika.</span><span class="sxs-lookup"><span data-stu-id="9e65e-110">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="9e65e-111">Identyfikator MPN partnera do zweryfikowania.</span><span class="sxs-lookup"><span data-stu-id="9e65e-111">The partner MPN ID to verify.</span></span> <span data-ttu-id="9e65e-112">Jeśli pominiesz tę wartość, żądanie pobierze profil MPN partnera, który się zalogował.</span><span class="sxs-lookup"><span data-stu-id="9e65e-112">If you omit this value, the request retrieves the MPN profile of the signed-in partner.</span></span>

## <a name="c"></a><span data-ttu-id="9e65e-113">C\#</span><span class="sxs-lookup"><span data-stu-id="9e65e-113">C\#</span></span>

<span data-ttu-id="9e65e-114">Aby zweryfikować identyfikator MPN partnera, najpierw pobierz interfejs do operacji zbierania profilów partnerów z właściwości [**IAggregatePartner.Profiles.**](/dotnet/api/microsoft.store.partnercenter.ipartner.profiles)</span><span class="sxs-lookup"><span data-stu-id="9e65e-114">To verify a partner's MPN ID, first retrieve an interface to partner profile collection operations from the [**IAggregatePartner.Profiles**](/dotnet/api/microsoft.store.partnercenter.ipartner.profiles) property.</span></span> <span data-ttu-id="9e65e-115">Następnie pobierz interfejs do operacji profilu MPN z właściwości [**MpnProfile.**](/dotnet/api/microsoft.store.partnercenter.profiles.ipartnerprofilecollection.mpnprofile)</span><span class="sxs-lookup"><span data-stu-id="9e65e-115">Then get an interface to MPN profile operations from the [**MpnProfile**](/dotnet/api/microsoft.store.partnercenter.profiles.ipartnerprofilecollection.mpnprofile) property.</span></span> <span data-ttu-id="9e65e-116">Na koniec wywołaj [**metody Get**](/dotnet/api/microsoft.store.partnercenter.profiles.impnprofile.get) lub [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.profiles.impnprofile.getasync) z identyfikatorem MPN, aby pobrać profil MPN.</span><span class="sxs-lookup"><span data-stu-id="9e65e-116">Finally, call the [**Get**](/dotnet/api/microsoft.store.partnercenter.profiles.impnprofile.get) or [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.profiles.impnprofile.getasync) methods with the MPN ID to retrieve the MPN profile.</span></span> <span data-ttu-id="9e65e-117">Jeśli pominiesz identyfikator MPN z wywołania Get lub GetAsync, żądanie podejmie próbę pobrania profilu MPN partnera, który się zalogował.</span><span class="sxs-lookup"><span data-stu-id="9e65e-117">If you omit the MPN ID from the Get or GetAsync call, the request attempts to retrieve the MPN profile of the signed-in partner.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// string partnerMpnId;

var partnerProfile = partnerOperations.Profiles.MpnProfile.Get(partnerMpnId);
```

<span data-ttu-id="9e65e-118">**Przykład:** [aplikacja testowa konsoli](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="9e65e-118">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="9e65e-119">**Project:** zestaw SDK Centrum partnerskiego Samples Class : VerifyPartnerMpnId.cs **(Klasa przykładów** zestaw SDK Centrum partnerskiego: VerifyPartnerMpnId.cs)</span><span class="sxs-lookup"><span data-stu-id="9e65e-119">**Project**: Partner Center SDK Samples **Class**: VerifyPartnerMpnId.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="9e65e-120">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="9e65e-120">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="9e65e-121">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="9e65e-121">Request syntax</span></span>

| <span data-ttu-id="9e65e-122">Metoda</span><span class="sxs-lookup"><span data-stu-id="9e65e-122">Method</span></span>  | <span data-ttu-id="9e65e-123">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="9e65e-123">Request URI</span></span>                                                                         |
|---------|-------------------------------------------------------------------------------------|
| <span data-ttu-id="9e65e-124">**Pobierz**</span><span class="sxs-lookup"><span data-stu-id="9e65e-124">**GET**</span></span> | <span data-ttu-id="9e65e-125">[*{baseURL}*](partner-center-rest-urls.md)/v1/profiles/mpn?mpnId={mpn-id} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="9e65e-125">[*{baseURL}*](partner-center-rest-urls.md)/v1/profiles/mpn?mpnId={mpn-id} HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="9e65e-126">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="9e65e-126">URI parameter</span></span>

<span data-ttu-id="9e65e-127">Podaj następujący parametr zapytania w celu zidentyfikowania partnera.</span><span class="sxs-lookup"><span data-stu-id="9e65e-127">Provide the following query parameter to identify the partner.</span></span> <span data-ttu-id="9e65e-128">Jeśli ten parametr zapytania zostanie pominięty, żądanie zwróci profil MPN partnera, który się zalogował.</span><span class="sxs-lookup"><span data-stu-id="9e65e-128">If you omit this query parameter, the request returns the MPN profile of the signed-in partner.</span></span>

| <span data-ttu-id="9e65e-129">Nazwa</span><span class="sxs-lookup"><span data-stu-id="9e65e-129">Name</span></span>   | <span data-ttu-id="9e65e-130">Typ</span><span class="sxs-lookup"><span data-stu-id="9e65e-130">Type</span></span> | <span data-ttu-id="9e65e-131">Wymagane</span><span class="sxs-lookup"><span data-stu-id="9e65e-131">Required</span></span> | <span data-ttu-id="9e65e-132">Opis</span><span class="sxs-lookup"><span data-stu-id="9e65e-132">Description</span></span>                                                 |
|--------|------|----------|-------------------------------------------------------------|
| <span data-ttu-id="9e65e-133">identyfikator mpn</span><span class="sxs-lookup"><span data-stu-id="9e65e-133">mpn-id</span></span> | <span data-ttu-id="9e65e-134">int</span><span class="sxs-lookup"><span data-stu-id="9e65e-134">int</span></span>  | <span data-ttu-id="9e65e-135">Nie</span><span class="sxs-lookup"><span data-stu-id="9e65e-135">No</span></span>       | <span data-ttu-id="9e65e-136">Identyfikator Microsoft Partner Network, który identyfikuje partnera.</span><span class="sxs-lookup"><span data-stu-id="9e65e-136">A Microsoft Partner Network ID that identifies the partner.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="9e65e-137">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="9e65e-137">Request headers</span></span>

<span data-ttu-id="9e65e-138">Aby uzyskać więcej informacji, [zobacz Partner Center REST headers (Nagłówki REST).](headers.md)</span><span class="sxs-lookup"><span data-stu-id="9e65e-138">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="9e65e-139">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="9e65e-139">Request body</span></span>

<span data-ttu-id="9e65e-140">Brak.</span><span class="sxs-lookup"><span data-stu-id="9e65e-140">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="9e65e-141">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="9e65e-141">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/profiles/mpn?mpnId=9999999 HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 560df6b9-6e53-4954-aed7-133477ac1194
MS-CorrelationId: e937630b-8341-4d70-8f73-450d32ee0189
X-Locale: en-US
MS-PartnerCenter-Client: Partner Center .NET SDK
Host: api.partnercenter.microsoft.com
Connection: Keep-Alive
```

## <a name="rest-response"></a><span data-ttu-id="9e65e-142">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="9e65e-142">REST response</span></span>

<span data-ttu-id="9e65e-143">Jeśli to się powiedzie, treść odpowiedzi zawiera [zasób MpnProfile](profile-resources.md#mpnprofile) dla partnera.</span><span class="sxs-lookup"><span data-stu-id="9e65e-143">If successful, the response body contains the [MpnProfile](profile-resources.md#mpnprofile) resource for the partner.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="9e65e-144">Kody powodzenia i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="9e65e-144">Response success and error codes</span></span>

<span data-ttu-id="9e65e-145">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie, oraz dodatkowe informacje o debugowaniu.</span><span class="sxs-lookup"><span data-stu-id="9e65e-145">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="9e65e-146">Użyj narzędzia śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="9e65e-146">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="9e65e-147">Aby uzyskać pełną listę, zobacz [Partner Center kody błędów REST.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="9e65e-147">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example-success"></a><span data-ttu-id="9e65e-148">Przykład odpowiedzi (powodzenie)</span><span class="sxs-lookup"><span data-stu-id="9e65e-148">Response example (success)</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 159
Content-Type: application/json; charset=utf-8
MS-CorrelationId: e937630b-8341-4d70-8f73-450d32ee0189
MS-RequestId: e39e0ddf-3fd0-4b7e-bb4e-8aebe242d3ee
MS-CV: s2GvkNgZsUSadxQX.0
MS-ServerId: 030011719
Date: Thu, 13 Apr 2017 18:13:40 GMT

{
    "mpnId": "4391507",
    "profileType": "MpnProfile",
    "links": {
        "self": {
            "uri": "/profiles/mpn",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "MpnProfile"
    }
}
```

### <a name="response-example-failure"></a><span data-ttu-id="9e65e-149">Przykład odpowiedzi (błąd)</span><span class="sxs-lookup"><span data-stu-id="9e65e-149">Response example (failure)</span></span>

```http
HTTP/1.1 404 Not Found
Content-Length: 124
Content-Type: application/json; charset=utf-8
MS-CorrelationId: e937630b-8341-4d70-8f73-450d32ee0189
MS-RequestId: 560df6b9-6e53-4954-aed7-133477ac1194
MS-CV: sLRFZMWm+EKuL47u.0
MS-ServerId: 102030524
Date: Thu, 13 Apr 2017 18:26:51 GMT

{
    "code": 3000,
    "description": "Partner Organization with partner_id 9999999 could not be found",
    "data": [],
    "source": "PartnerFD"
}
```
