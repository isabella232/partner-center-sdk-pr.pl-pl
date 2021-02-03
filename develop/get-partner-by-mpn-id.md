---
title: Weryfikowanie identyfikatora MPN partnera
description: Dowiedz się, jak zweryfikować identyfikator Microsoft Partner Network partnera (identyfikator MPN), żądając profilu MPN partnera za pośrednictwem usługi C \# lub interfejsu API REST Centrum partnerskiego.
ms.date: 09/29/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 6ef7bcb35274a6bcbaddbe0553ca0cb4dc1b2f9c
ms.sourcegitcommit: 8a5c37376a29e29fe0002a980082d4acc6b91131
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/11/2020
ms.locfileid: "97768501"
---
# <a name="verify-a-partner-mpn-id-via-c-or-the-partner-center-rest-api"></a><span data-ttu-id="58a7b-103">Weryfikowanie identyfikatora MPN partnera za pośrednictwem języka C \# lub interfejsu API REST Centrum partnerskiego</span><span class="sxs-lookup"><span data-stu-id="58a7b-103">Verify a partner MPN ID via C\# or the Partner Center REST API</span></span>

<span data-ttu-id="58a7b-104">**Dotyczy**</span><span class="sxs-lookup"><span data-stu-id="58a7b-104">**Applies To**</span></span>

- <span data-ttu-id="58a7b-105">Centrum partnerskie</span><span class="sxs-lookup"><span data-stu-id="58a7b-105">Partner Center</span></span>
- <span data-ttu-id="58a7b-106">Centrum partnerskie obsługiwane przez firmę 21Vianet</span><span class="sxs-lookup"><span data-stu-id="58a7b-106">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="58a7b-107">Centrum partnerskie dla Microsoft Cloud Niemcy</span><span class="sxs-lookup"><span data-stu-id="58a7b-107">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="58a7b-108">Centrum partnerskie Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="58a7b-108">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="58a7b-109">Weryfikowanie identyfikatora Microsoft Partner Network partnera (identyfikator MPN).</span><span class="sxs-lookup"><span data-stu-id="58a7b-109">How to verify a partner's Microsoft Partner Network identifier (MPN ID).</span></span>

<span data-ttu-id="58a7b-110">Pokazana tutaj technika sprawdza identyfikator Microsoft Partner Network partnera, żądając profilu MPN partnera od centrum partnerskiego.</span><span class="sxs-lookup"><span data-stu-id="58a7b-110">The technique shown here verifies the partner's Microsoft Partner Network identifier by requesting the partner's MPN profile from partner center.</span></span> <span data-ttu-id="58a7b-111">Identyfikator jest uznawany za ważny, jeśli żądanie zakończy się pomyślnie.</span><span class="sxs-lookup"><span data-stu-id="58a7b-111">The identifier is considered valid if the request succeeds.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="58a7b-112">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="58a7b-112">Prerequisites</span></span>

- <span data-ttu-id="58a7b-113">Poświadczenia zgodnie z opisem w temacie [uwierzytelnianie w centrum partnerskim](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="58a7b-113">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="58a7b-114">Ten scenariusz obsługuje tylko uwierzytelnianie przy użyciu aplikacji i poświadczeń użytkownika.</span><span class="sxs-lookup"><span data-stu-id="58a7b-114">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="58a7b-115">IDENTYFIKATOR MPN partnera do zweryfikowania.</span><span class="sxs-lookup"><span data-stu-id="58a7b-115">The partner MPN ID to verify.</span></span> <span data-ttu-id="58a7b-116">W przypadku pominięcia tej wartości żądanie pobiera profil MPN zalogowanego partnera.</span><span class="sxs-lookup"><span data-stu-id="58a7b-116">If you omit this value, the request retrieves the MPN profile of the signed-in partner.</span></span>

## <a name="c"></a><span data-ttu-id="58a7b-117">C\#</span><span class="sxs-lookup"><span data-stu-id="58a7b-117">C\#</span></span>

<span data-ttu-id="58a7b-118">Aby sprawdzić identyfikator MPN partnera, najpierw Pobierz interfejs na potrzeby operacji zbierania profilów partnera z właściwości [**IAggregatePartner. profile**](/dotnet/api/microsoft.store.partnercenter.ipartner.profiles) .</span><span class="sxs-lookup"><span data-stu-id="58a7b-118">To verify a partner's MPN ID, first retrieve an interface to partner profile collection operations from the [**IAggregatePartner.Profiles**](/dotnet/api/microsoft.store.partnercenter.ipartner.profiles) property.</span></span> <span data-ttu-id="58a7b-119">Następnie uzyskaj interfejs do MPN operacji profilu z właściwości [**MpnProfile**](/dotnet/api/microsoft.store.partnercenter.profiles.ipartnerprofilecollection.mpnprofile) .</span><span class="sxs-lookup"><span data-stu-id="58a7b-119">Then get an interface to MPN profile operations from the [**MpnProfile**](/dotnet/api/microsoft.store.partnercenter.profiles.ipartnerprofilecollection.mpnprofile) property.</span></span> <span data-ttu-id="58a7b-120">Na koniec wywołaj metody [**Get**](/dotnet/api/microsoft.store.partnercenter.profiles.impnprofile.get) lub [**GETasync**](/dotnet/api/microsoft.store.partnercenter.profiles.impnprofile.getasync) z identyfikatorem MPN, aby pobrać profil MPN.</span><span class="sxs-lookup"><span data-stu-id="58a7b-120">Finally, call the [**Get**](/dotnet/api/microsoft.store.partnercenter.profiles.impnprofile.get) or [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.profiles.impnprofile.getasync) methods with the MPN ID to retrieve the MPN profile.</span></span> <span data-ttu-id="58a7b-121">W przypadku pominięcia identyfikatora MPN z wywołania get lub GetAsync żądanie próbuje pobrać profil MPN partnera zalogowanego.</span><span class="sxs-lookup"><span data-stu-id="58a7b-121">If you omit the MPN ID from the Get or GetAsync call, the request attempts to retrieve the MPN profile of the signed-in partner.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// string partnerMpnId;

var partnerProfile = partnerOperations.Profiles.MpnProfile.Get(partnerMpnId);
```

<span data-ttu-id="58a7b-122">**Przykład**: [aplikacja testowa konsoli](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="58a7b-122">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="58a7b-123">**Projekt**: **Klasa** przykładów zestawu SDK centrum partnerskiego: VerifyPartnerMpnId.cs</span><span class="sxs-lookup"><span data-stu-id="58a7b-123">**Project**: Partner Center SDK Samples **Class**: VerifyPartnerMpnId.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="58a7b-124">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="58a7b-124">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="58a7b-125">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="58a7b-125">Request syntax</span></span>

| <span data-ttu-id="58a7b-126">Metoda</span><span class="sxs-lookup"><span data-stu-id="58a7b-126">Method</span></span>  | <span data-ttu-id="58a7b-127">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="58a7b-127">Request URI</span></span>                                                                         |
|---------|-------------------------------------------------------------------------------------|
| <span data-ttu-id="58a7b-128">**Pobierz**</span><span class="sxs-lookup"><span data-stu-id="58a7b-128">**GET**</span></span> | <span data-ttu-id="58a7b-129">[*{baseURL}*](partner-center-rest-urls.md)/V1/Profiles/MPN? mpnId = {MPN-ID} http/1.1</span><span class="sxs-lookup"><span data-stu-id="58a7b-129">[*{baseURL}*](partner-center-rest-urls.md)/v1/profiles/mpn?mpnId={mpn-id} HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="58a7b-130">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="58a7b-130">URI parameter</span></span>

<span data-ttu-id="58a7b-131">Podaj następujący parametr zapytania, aby zidentyfikować partnera.</span><span class="sxs-lookup"><span data-stu-id="58a7b-131">Provide the following query parameter to identify the partner.</span></span> <span data-ttu-id="58a7b-132">Jeśli pominięto ten parametr zapytania, żądanie zwróci profil MPN zalogowanego partnera.</span><span class="sxs-lookup"><span data-stu-id="58a7b-132">If you omit this query parameter, the request returns the MPN profile of the signed-in partner.</span></span>

| <span data-ttu-id="58a7b-133">Nazwa</span><span class="sxs-lookup"><span data-stu-id="58a7b-133">Name</span></span>   | <span data-ttu-id="58a7b-134">Typ</span><span class="sxs-lookup"><span data-stu-id="58a7b-134">Type</span></span> | <span data-ttu-id="58a7b-135">Wymagane</span><span class="sxs-lookup"><span data-stu-id="58a7b-135">Required</span></span> | <span data-ttu-id="58a7b-136">Opis</span><span class="sxs-lookup"><span data-stu-id="58a7b-136">Description</span></span>                                                 |
|--------|------|----------|-------------------------------------------------------------|
| <span data-ttu-id="58a7b-137">MPN — identyfikator</span><span class="sxs-lookup"><span data-stu-id="58a7b-137">mpn-id</span></span> | <span data-ttu-id="58a7b-138">int</span><span class="sxs-lookup"><span data-stu-id="58a7b-138">int</span></span>  | <span data-ttu-id="58a7b-139">Nie</span><span class="sxs-lookup"><span data-stu-id="58a7b-139">No</span></span>       | <span data-ttu-id="58a7b-140">Identyfikator Microsoft Partner Network, który identyfikuje partnera.</span><span class="sxs-lookup"><span data-stu-id="58a7b-140">A Microsoft Partner Network ID that identifies the partner.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="58a7b-141">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="58a7b-141">Request headers</span></span>

<span data-ttu-id="58a7b-142">Aby uzyskać więcej informacji, zobacz [nagłówki REST Centrum partnerskiego](headers.md).</span><span class="sxs-lookup"><span data-stu-id="58a7b-142">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="58a7b-143">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="58a7b-143">Request body</span></span>

<span data-ttu-id="58a7b-144">Brak.</span><span class="sxs-lookup"><span data-stu-id="58a7b-144">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="58a7b-145">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="58a7b-145">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="58a7b-146">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="58a7b-146">REST response</span></span>

<span data-ttu-id="58a7b-147">Jeśli to się powiedzie, treść odpowiedzi zawiera zasób [MpnProfile](profile-resources.md#mpnprofile) dla partnera.</span><span class="sxs-lookup"><span data-stu-id="58a7b-147">If successful, the response body contains the [MpnProfile](profile-resources.md#mpnprofile) resource for the partner.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="58a7b-148">Kody sukcesu i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="58a7b-148">Response success and error codes</span></span>

<span data-ttu-id="58a7b-149">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie i dodatkowe informacje debugowania.</span><span class="sxs-lookup"><span data-stu-id="58a7b-149">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="58a7b-150">Użyj narzędzia do śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="58a7b-150">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="58a7b-151">Aby uzyskać pełną listę, zobacz [kody błędów REST centrum partnera](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="58a7b-151">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example-success"></a><span data-ttu-id="58a7b-152">Przykład odpowiedzi (powodzenie)</span><span class="sxs-lookup"><span data-stu-id="58a7b-152">Response example (success)</span></span>

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

### <a name="response-example-failure"></a><span data-ttu-id="58a7b-153">Przykład odpowiedzi (niepowodzenie)</span><span class="sxs-lookup"><span data-stu-id="58a7b-153">Response example (failure)</span></span>

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
