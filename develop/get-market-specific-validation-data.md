---
title: Pobieranie reguł formatowania adresów według rynku
description: Uzyskaj oczekiwany format adresu na podstawie kodu ISO dla rynku.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: d5233d059ea6e71c28df36b2242659c28c5dd857
ms.sourcegitcommit: b307fd75e305e0a88cfd1182cc01d2c9a108ce45
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/06/2021
ms.locfileid: "111549046"
---
# <a name="get-address-formatting-rules-by-market"></a><span data-ttu-id="cf3aa-103">Pobieranie reguł formatowania adresów według rynku</span><span class="sxs-lookup"><span data-stu-id="cf3aa-103">Get address formatting rules by market</span></span>

<span data-ttu-id="cf3aa-104">**Dotyczy:** Partner Center | Partner Center obsługiwana przez firmę 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="cf3aa-104">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>


<span data-ttu-id="cf3aa-105">Uzyskaj oczekiwany format adresu na podstawie kodu ISO dla rynku.</span><span class="sxs-lookup"><span data-stu-id="cf3aa-105">Get the expected address format based on the iso code for the market.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="cf3aa-106">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="cf3aa-106">Prerequisites</span></span>

- <span data-ttu-id="cf3aa-107">Poświadczenia zgodnie z opisem w te [Partner Center uwierzytelniania.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="cf3aa-107">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="cf3aa-108">Ten scenariusz obsługuje uwierzytelnianie przy użyciu zarówno poświadczeń aplikacji autonomicznej, jak i aplikacji i użytkownika.</span><span class="sxs-lookup"><span data-stu-id="cf3aa-108">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

## <a name="rest-request"></a><span data-ttu-id="cf3aa-109">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="cf3aa-109">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="cf3aa-110">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="cf3aa-110">Request syntax</span></span>

| <span data-ttu-id="cf3aa-111">Metoda</span><span class="sxs-lookup"><span data-stu-id="cf3aa-111">Method</span></span>  | <span data-ttu-id="cf3aa-112">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="cf3aa-112">Request URI</span></span>                                                                                 |
|---------|---------------------------------------------------------------------------------------------|
| <span data-ttu-id="cf3aa-113">**Pobierz**</span><span class="sxs-lookup"><span data-stu-id="cf3aa-113">**GET**</span></span> | <span data-ttu-id="cf3aa-114">[*{baseURL}*](partner-center-rest-urls.md)/v1/countryvalidationrules/{isocode-id} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="cf3aa-114">[*{baseURL}*](partner-center-rest-urls.md)/v1/countryvalidationrules/{isocode-id} HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="cf3aa-115">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="cf3aa-115">URI parameter</span></span>

| <span data-ttu-id="cf3aa-116">Nazwa</span><span class="sxs-lookup"><span data-stu-id="cf3aa-116">Name</span></span>           | <span data-ttu-id="cf3aa-117">Typ</span><span class="sxs-lookup"><span data-stu-id="cf3aa-117">Type</span></span>       | <span data-ttu-id="cf3aa-118">Wymagane</span><span class="sxs-lookup"><span data-stu-id="cf3aa-118">Required</span></span> | <span data-ttu-id="cf3aa-119">Opis</span><span class="sxs-lookup"><span data-stu-id="cf3aa-119">Description</span></span>                         |
|----------------|------------|----------|-------------------------------------|
| <span data-ttu-id="cf3aa-120">**identyfikator isocode**</span><span class="sxs-lookup"><span data-stu-id="cf3aa-120">**isocode-id**</span></span> | <span data-ttu-id="cf3aa-121">**ciąg**</span><span class="sxs-lookup"><span data-stu-id="cf3aa-121">**string**</span></span> | <span data-ttu-id="cf3aa-122">Y</span><span class="sxs-lookup"><span data-stu-id="cf3aa-122">Y</span></span>        | <span data-ttu-id="cf3aa-123">Dwue znakowy kod kraju ISO.</span><span class="sxs-lookup"><span data-stu-id="cf3aa-123">The two-character ISO country code.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="cf3aa-124">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="cf3aa-124">Request headers</span></span>

<span data-ttu-id="cf3aa-125">Aby uzyskać więcej informacji, [zobacz Partner Center REST headers (Nagłówki REST).](headers.md)</span><span class="sxs-lookup"><span data-stu-id="cf3aa-125">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="cf3aa-126">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="cf3aa-126">Request body</span></span>

<span data-ttu-id="cf3aa-127">Brak.</span><span class="sxs-lookup"><span data-stu-id="cf3aa-127">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="cf3aa-128">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="cf3aa-128">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/countryvalidationrules/{isocode-id} HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 124b0e41-a093-4fec-b871-3eeb45fd734b
MS-CorrelationId: 5cfd634d-b936-47af-87f0-0f0217425dcc
```

## <a name="rest-response"></a><span data-ttu-id="cf3aa-129">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="cf3aa-129">REST response</span></span>

<span data-ttu-id="cf3aa-130">W przypadku powodzenia ta metoda zwraca **obiekt CountryInformation** w treści odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="cf3aa-130">If successful, this method returns a **CountryInformation** object in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="cf3aa-131">Kody powodzenia i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="cf3aa-131">Response success and error codes</span></span>

<span data-ttu-id="cf3aa-132">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie, oraz dodatkowe informacje o debugowaniu.</span><span class="sxs-lookup"><span data-stu-id="cf3aa-132">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="cf3aa-133">Użyj narzędzia śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="cf3aa-133">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="cf3aa-134">Aby uzyskać pełną listę, zobacz [Kody błędów](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="cf3aa-134">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="cf3aa-135">Przykład odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="cf3aa-135">Response example</span></span>

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
