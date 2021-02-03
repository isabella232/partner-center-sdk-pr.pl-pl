---
title: Pobieranie reguł formatowania adresów według rynku
description: Pobierz oczekiwany format adresu na podstawie kodu ISO dla rynku.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: c755a38c11ed9803edb7777a0f661c1fbc5a6107
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/08/2020
ms.locfileid: "97767878"
---
# <a name="get-address-formatting-rules-by-market"></a><span data-ttu-id="89a24-103">Pobieranie reguł formatowania adresów według rynku</span><span class="sxs-lookup"><span data-stu-id="89a24-103">Get address formatting rules by market</span></span>

<span data-ttu-id="89a24-104">**Dotyczy**</span><span class="sxs-lookup"><span data-stu-id="89a24-104">**Applies To**</span></span>

- <span data-ttu-id="89a24-105">Centrum partnerskie</span><span class="sxs-lookup"><span data-stu-id="89a24-105">Partner Center</span></span>
- <span data-ttu-id="89a24-106">Centrum partnerskie obsługiwane przez firmę 21Vianet</span><span class="sxs-lookup"><span data-stu-id="89a24-106">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="89a24-107">Centrum partnerskie dla Microsoft Cloud Niemcy</span><span class="sxs-lookup"><span data-stu-id="89a24-107">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="89a24-108">Centrum partnerskie Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="89a24-108">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="89a24-109">Pobierz oczekiwany format adresu na podstawie kodu ISO dla rynku.</span><span class="sxs-lookup"><span data-stu-id="89a24-109">Get the expected address format based on the iso code for the market.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="89a24-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="89a24-110">Prerequisites</span></span>

- <span data-ttu-id="89a24-111">Poświadczenia zgodnie z opisem w temacie [uwierzytelnianie w centrum partnerskim](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="89a24-111">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="89a24-112">Ten scenariusz obsługuje uwierzytelnianie zarówno w przypadku aplikacji autonomicznych, jak i aplikacji oraz poświadczeń użytkownika.</span><span class="sxs-lookup"><span data-stu-id="89a24-112">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

## <a name="rest-request"></a><span data-ttu-id="89a24-113">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="89a24-113">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="89a24-114">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="89a24-114">Request syntax</span></span>

| <span data-ttu-id="89a24-115">Metoda</span><span class="sxs-lookup"><span data-stu-id="89a24-115">Method</span></span>  | <span data-ttu-id="89a24-116">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="89a24-116">Request URI</span></span>                                                                                 |
|---------|---------------------------------------------------------------------------------------------|
| <span data-ttu-id="89a24-117">**Pobierz**</span><span class="sxs-lookup"><span data-stu-id="89a24-117">**GET**</span></span> | <span data-ttu-id="89a24-118">[*{baseURL}*](partner-center-rest-urls.md)/V1/countryvalidationrules/{isoCode-ID} http/1.1</span><span class="sxs-lookup"><span data-stu-id="89a24-118">[*{baseURL}*](partner-center-rest-urls.md)/v1/countryvalidationrules/{isocode-id} HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="89a24-119">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="89a24-119">URI parameter</span></span>

| <span data-ttu-id="89a24-120">Nazwa</span><span class="sxs-lookup"><span data-stu-id="89a24-120">Name</span></span>           | <span data-ttu-id="89a24-121">Typ</span><span class="sxs-lookup"><span data-stu-id="89a24-121">Type</span></span>       | <span data-ttu-id="89a24-122">Wymagane</span><span class="sxs-lookup"><span data-stu-id="89a24-122">Required</span></span> | <span data-ttu-id="89a24-123">Opis</span><span class="sxs-lookup"><span data-stu-id="89a24-123">Description</span></span>                         |
|----------------|------------|----------|-------------------------------------|
| <span data-ttu-id="89a24-124">**isoCode — identyfikator**</span><span class="sxs-lookup"><span data-stu-id="89a24-124">**isocode-id**</span></span> | <span data-ttu-id="89a24-125">**parametry**</span><span class="sxs-lookup"><span data-stu-id="89a24-125">**string**</span></span> | <span data-ttu-id="89a24-126">Y</span><span class="sxs-lookup"><span data-stu-id="89a24-126">Y</span></span>        | <span data-ttu-id="89a24-127">Dwuznakowy kod ISO kraju.</span><span class="sxs-lookup"><span data-stu-id="89a24-127">The two-character ISO country code.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="89a24-128">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="89a24-128">Request headers</span></span>

<span data-ttu-id="89a24-129">Aby uzyskać więcej informacji, zobacz [nagłówki REST Centrum partnerskiego](headers.md).</span><span class="sxs-lookup"><span data-stu-id="89a24-129">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="89a24-130">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="89a24-130">Request body</span></span>

<span data-ttu-id="89a24-131">Brak.</span><span class="sxs-lookup"><span data-stu-id="89a24-131">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="89a24-132">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="89a24-132">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/countryvalidationrules/{isocode-id} HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 124b0e41-a093-4fec-b871-3eeb45fd734b
MS-CorrelationId: 5cfd634d-b936-47af-87f0-0f0217425dcc
```

## <a name="rest-response"></a><span data-ttu-id="89a24-133">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="89a24-133">REST response</span></span>

<span data-ttu-id="89a24-134">Jeśli to się powiedzie, metoda zwraca obiekt **CountryInformation** w treści odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="89a24-134">If successful, this method returns a **CountryInformation** object in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="89a24-135">Kody sukcesu i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="89a24-135">Response success and error codes</span></span>

<span data-ttu-id="89a24-136">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie i dodatkowe informacje debugowania.</span><span class="sxs-lookup"><span data-stu-id="89a24-136">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="89a24-137">Użyj narzędzia do śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="89a24-137">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="89a24-138">Aby uzyskać pełną listę, zobacz [kody błędów](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="89a24-138">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="89a24-139">Przykład odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="89a24-139">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 1856
Content-Type: application/json
MS-CorrelationId: 5cfd634d-b936-47af-87f0-0f0217425dcc
MS-RequestId: 124b0e41-a093-4fec-b871-3eeb45fd734b
Date: Wed, 25 Nov 2015 06:36:47 GMT

{
    "iso2Code": "US",
    "defaultCulture": "en-US",
    "isStateRequired": true,
    "states": {
        "value": ["AK","AL","AR", "AZ","CA","CO","CT","DC","DE","FL","GA","HI","IA","ID","IL","IN",
        "KS","KY","LA","MA","MD","ME","MI","MN","MO","MS","MT","NC","ND","NE","NH","NJ","NM","NV",
        "NY","OH","OK","OR","PA","RI","SC","SD","TN","TX","UT","VA","VT","WA","WI","WV","WY"]
    },
    "supportedLanguages": {
        "value": ["en",
        "es"]
    },
    "supportedCultures": {
        "value": ["en-US",
        "es-US"]
    },
    "isPostalCodeRequired": true,
    "postalCodeRegex": "^\\d{
        5
    }(-\\d{
        4
    })?$",
    "isCityRequired": true,
    "isVatIdSupported": false,
    "taxIdFormat": "US######",
    "taxIdSample": "US999965",
    "phoneNumberRegex": "^(1[\\-\\/\\.]?)?(\((\\d{3})\)|(\\d{3}))[\\-\\/\\.]?(\\d{3})[\\-\\/\\.]?(\\d{4})$",
    "isRegistrationNumberSupported": false,
    "isTaxIdSupported": true,
    "resellerAgreementRegion": "AOC",
    "geographicRegion": "NorthAndLatinAmerica",
    "countryCallingCodes": {
        "value": ["1"]
    },
    "attributes": {
        "objectType": "CountryInformation"
    }
}
```
