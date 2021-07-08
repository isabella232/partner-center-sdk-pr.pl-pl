---
title: Pobieranie dodatków dla identyfikatora oferty
description: Jak uzyskać dodatki dla identyfikatora oferty.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: rbars
ms.author: rbars
ms.openlocfilehash: e3b0ab8007d3affa6912479b960f6dae3bc0bd28
ms.sourcegitcommit: d4b0c80d81f1d5bdf3c4c03344ad639646ae6ab9
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/09/2021
ms.locfileid: "111760338"
---
# <a name="get-add-ons-for-an-offer-id"></a><span data-ttu-id="615df-103">Pobieranie dodatków dla identyfikatora oferty</span><span class="sxs-lookup"><span data-stu-id="615df-103">Get add-ons for an offer ID</span></span>

<span data-ttu-id="615df-104">**Dotyczy:** Partner Center | Partner Center obsługiwana przez firmę 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="615df-104">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="615df-105">Jak uzyskać dodatki dla identyfikatora oferty.</span><span class="sxs-lookup"><span data-stu-id="615df-105">How to get the add-ons for an offer ID.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="615df-106">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="615df-106">Prerequisites</span></span>

- <span data-ttu-id="615df-107">Poświadczenia zgodnie z opisem w te [Partner Center uwierzytelniania.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="615df-107">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="615df-108">Ten scenariusz obsługuje uwierzytelnianie przy użyciu zarówno poświadczeń aplikacji autonomicznej, jak i aplikacji i użytkownika.</span><span class="sxs-lookup"><span data-stu-id="615df-108">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="615df-109">Identyfikator oferty.</span><span class="sxs-lookup"><span data-stu-id="615df-109">An offer ID.</span></span> <span data-ttu-id="615df-110">Jeśli nie masz identyfikatora oferty, zobacz Get a list of offers for a market (Uzyskiwanie listy [ofert dla rynku).](get-a-list-of-offers-for-a-market.md)</span><span class="sxs-lookup"><span data-stu-id="615df-110">If you don't have the offer ID, see [Get a list of offers for a market](get-a-list-of-offers-for-a-market.md).</span></span>

## <a name="c"></a><span data-ttu-id="615df-111">C\#</span><span class="sxs-lookup"><span data-stu-id="615df-111">C\#</span></span>

<span data-ttu-id="615df-112">Aby uzyskać dodatki dla oferty według identyfikatora, najpierw wywołaj metodę [**IAggregatePartner.Offers.ByCountry**](/dotnet/api/microsoft.store.partnercenter.genericoperations.icountryselector-1.bycountry) z kodem kraju, aby uzyskać interfejs do zaoferowania operacji na podstawie danego kraju.</span><span class="sxs-lookup"><span data-stu-id="615df-112">To get the add-ons for an offer by ID, first call the [**IAggregatePartner.Offers.ByCountry**](/dotnet/api/microsoft.store.partnercenter.genericoperations.icountryselector-1.bycountry) method with the country code to get an interface to offer operations based on the given country.</span></span> <span data-ttu-id="615df-113">Następnie wywołaj [**metodę ByID**](/dotnet/api/microsoft.store.partnercenter.offers.ioffercollection.byid) z identyfikatorem oferty, aby zidentyfikować ofertę, której dodatki chcesz pobrać.</span><span class="sxs-lookup"><span data-stu-id="615df-113">Then call the [**ByID**](/dotnet/api/microsoft.store.partnercenter.offers.ioffercollection.byid) method with the offer ID to identify the offer whose add-ons you want to retrieve.</span></span> <span data-ttu-id="615df-114">Następnie użyj właściwości [**AddOns,**](/dotnet/api/microsoft.store.partnercenter.offers.ioffer.addons) aby uzyskać interfejs do operacji dodatku dla bieżącej oferty.</span><span class="sxs-lookup"><span data-stu-id="615df-114">Next, use the [**AddOns**](/dotnet/api/microsoft.store.partnercenter.offers.ioffer.addons) property to get an interface to add-on operations for the current offer.</span></span> <span data-ttu-id="615df-115">Na koniec wywołaj [**metodę Get**](/dotnet/api/microsoft.store.partnercenter.offers.iofferaddons.get) lub [**GetAsync,**](/dotnet/api/microsoft.store.partnercenter.offers.iofferaddons.getasync) aby pobrać kolekcję wszystkich dodatków dla określonej oferty.</span><span class="sxs-lookup"><span data-stu-id="615df-115">Finally, call the [**Get**](/dotnet/api/microsoft.store.partnercenter.offers.iofferaddons.get) or [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.offers.iofferaddons.getasync) method to get a collection of all the add-ons for the specified offer.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// string offerId;
// string countryCode;

var offerAddOns = partnerOperations.Offers.ByCountry(countryCode).ById(offerId).AddOns.Get();
```

<span data-ttu-id="615df-116">**Przykład:** [aplikacja testowa konsoli](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="615df-116">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="615df-117">**Project:** zestaw SDK Centrum partnerskiego Samples Class : GetOffer.cs **(Klasa przykładów** zestaw SDK Centrum partnerskiego: GetOffer.cs)</span><span class="sxs-lookup"><span data-stu-id="615df-117">**Project**: Partner Center SDK Samples **Class**: GetOffer.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="615df-118">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="615df-118">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="615df-119">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="615df-119">Request syntax</span></span>

| <span data-ttu-id="615df-120">Metoda</span><span class="sxs-lookup"><span data-stu-id="615df-120">Method</span></span>  | <span data-ttu-id="615df-121">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="615df-121">Request URI</span></span>                                                                                             |
|---------|---------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="615df-122">**Pobierz**</span><span class="sxs-lookup"><span data-stu-id="615df-122">**GET**</span></span> | <span data-ttu-id="615df-123">[*{baseURL}*](partner-center-rest-urls.md)/v1/offers/{identyfikator oferty}/addons?country={country-code} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="615df-123">[*{baseURL}*](partner-center-rest-urls.md)/v1/offers/{offer-id}/addons?country={country-code} HTTP/1.1</span></span> |

### <a name="uri-parameters"></a><span data-ttu-id="615df-124">Parametry URI</span><span class="sxs-lookup"><span data-stu-id="615df-124">URI parameters</span></span>

<span data-ttu-id="615df-125">Użyj następujących parametrów, aby podać identyfikator oferty i kod kraju.</span><span class="sxs-lookup"><span data-stu-id="615df-125">Use the following parameters to provide the offer ID and country code.</span></span>

| <span data-ttu-id="615df-126">Nazwa</span><span class="sxs-lookup"><span data-stu-id="615df-126">Name</span></span>         | <span data-ttu-id="615df-127">Typ</span><span class="sxs-lookup"><span data-stu-id="615df-127">Type</span></span>       | <span data-ttu-id="615df-128">Wymagane</span><span class="sxs-lookup"><span data-stu-id="615df-128">Required</span></span> | <span data-ttu-id="615df-129">Opis</span><span class="sxs-lookup"><span data-stu-id="615df-129">Description</span></span>                       |
|--------------|------------|----------|-----------------------------------|
| <span data-ttu-id="615df-130">**identyfikator oferty**</span><span class="sxs-lookup"><span data-stu-id="615df-130">**offer-id**</span></span> | <span data-ttu-id="615df-131">**guid**</span><span class="sxs-lookup"><span data-stu-id="615df-131">**guid**</span></span>   | <span data-ttu-id="615df-132">Y</span><span class="sxs-lookup"><span data-stu-id="615df-132">Y</span></span>        | <span data-ttu-id="615df-133">Identyfikator GUID, który identyfikuje ofertę.</span><span class="sxs-lookup"><span data-stu-id="615df-133">A GUID that identifies the offer.</span></span> |
| <span data-ttu-id="615df-134">**Kraju**</span><span class="sxs-lookup"><span data-stu-id="615df-134">**country**</span></span>  | <span data-ttu-id="615df-135">**ciąg**</span><span class="sxs-lookup"><span data-stu-id="615df-135">**string**</span></span> | <span data-ttu-id="615df-136">Y</span><span class="sxs-lookup"><span data-stu-id="615df-136">Y</span></span>        | <span data-ttu-id="615df-137">Kod kraju (na przykład `US` ).</span><span class="sxs-lookup"><span data-stu-id="615df-137">The country code (for example `US`).</span></span>       |

### <a name="request-headers"></a><span data-ttu-id="615df-138">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="615df-138">Request headers</span></span>

<span data-ttu-id="615df-139">Aby uzyskać więcej informacji, [zobacz Partner Center REST headers (Nagłówki REST).](headers.md)</span><span class="sxs-lookup"><span data-stu-id="615df-139">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="615df-140">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="615df-140">Request body</span></span>

<span data-ttu-id="615df-141">Brak.</span><span class="sxs-lookup"><span data-stu-id="615df-141">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="615df-142">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="615df-142">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/offers/195416C1-3447-423A-B37B-EE59A99A19C4/addons?country=us HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: c15e829e-ecc7-42c2-8a4b-5e6961f4e3f8
MS-CorrelationId: 26d2b3b1-c76a-4aeb-8298-1654c91d9eb8
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a><span data-ttu-id="615df-143">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="615df-143">REST response</span></span>

<span data-ttu-id="615df-144">W przypadku powodzenia ta metoda zwraca kolekcję [obiektów Offer](offer-resources.md) w treści odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="615df-144">If successful, this method returns a collection of [Offer](offer-resources.md) objects in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="615df-145">Kody powodzenia i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="615df-145">Response success and error codes</span></span>

<span data-ttu-id="615df-146">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie, oraz dodatkowe informacje o debugowaniu.</span><span class="sxs-lookup"><span data-stu-id="615df-146">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="615df-147">Użyj narzędzia śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="615df-147">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="615df-148">Aby uzyskać pełną listę, zobacz [Partner Center kodów błędów REST.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="615df-148">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="615df-149">Przykład odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="615df-149">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 3137
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 26d2b3b1-c76a-4aeb-8298-1654c91d9eb8
MS-RequestId: c15e829e-ecc7-42c2-8a4b-5e6961f4e3f8
MS-CV: P8xjUcSeY0ithZ9S.0
MS-ServerId: 202010406
Date: Wed, 01 Feb 2017 22:37:58 GMT

{
    "totalCount": 2,
    "items": [{
            "id": "2828BE95-46BA-4F91-B2FD-0BEF192ECF60",
            "name": "Exchange Online Archiving for Exchange Online",
            "description": "A personal e-mail archive for users who have mailboxes on Exchange Server 2010 or later.",
            "minimumQuantity": 1,
            "maximumQuantity": 10000000,
            "rank": 200,
            "uri": "/3c95518e-8c37-41e3-9627-0ca339200f53/Offers/2828BE95-46BA-4F91-B2FD-0BEF192ECF60",
            "locale": "en-US",
            "country": "US",
            "category": {
                "id": "",
                "name": "",
                "rank": 0,
                "locale": "en-us",
                "country": "US",
                "attributes": {
                    "objectType": "OfferCategory"
                }
            },
            "prerequisiteOffers": ["35A36B80-270A-44BF-9290-00545D350866", "6FBAD345-B7DE-42A6-B6AB-79B363D0B371", "91FD106F-4B2C-4938-95AC-F54F74E9A239", "195416C1-3447-423A-B37B-EE59A99A19C4", "22A70120-4078-4926-9592-39ED91CB9C01", "2A727AE4-F201-497D-A9D6-C6A892DF4A87", "BD938F12-058F-4927-BBA3-AE36B1D2501C", "031C9E47-4802-4248-838E-778FB1D2CC05", "B2016E73-D9AD-4758-B8B8-D5C001BDF411", "AA98032C-5403-472F-B24F-F6654846B15D"],
            "isAddOn": true,
            "isAvailableForPurchase": true,
            "billing": "license",
            "isAutoRenewable": true,
            "salesGroupId": "1",
            "product": {
                "id": "EE02FD1B-340E-4A4B-B355-4A514E4C8943",
                "name": "Exchange Online Archiving for Exchange Online",
                "unit": "Licenses"
            },
            "unitType": "Licenses",
            "links": {
                "learnMore": {
                    "uri": "http://g.microsoftonline.com/0BXPS00en-us/1302",
                    "method": "GET",
                    "headers": []
                },
                "self": {
                    "uri": "/offers/2828BE95-46BA-4F91-B2FD-0BEF192ECF60?country=US",
                    "method": "GET",
                    "headers": []
                }
            },
            "attributes": {
                "objectType": "Offer"
            }
        }, {
            "id": "45320EC9-9B8E-49D0-B900-F14141A0ABD1",
            "name": "Microsoft MyAnalytics",
            "description": "Microsoft MyAnalytics provides insights about time and relationships to help individuals and teams achieve more at work.",
            "minimumQuantity": 1,
            "maximumQuantity": 10000000,
            "rank": 232,
            "uri": "/3c95518e-8c37-41e3-9627-0ca339200f53/Offers/45320EC9-9B8E-49D0-B900-F14141A0ABD1",
            "locale": "en-US",
            "country": "US",
            "category": {
                "id": "",
                "name": "",
                "rank": 0,
                "locale": "en-us",
                "country": "US",
                "attributes": {
                    "objectType": "OfferCategory"
                }
            },
            "prerequisiteOffers": ["195416C1-3447-423A-B37B-EE59A99A19C4", "2F707C7C-2433-49A5-A437-9CA7CF40D3EB", "91FD106F-4B2C-4938-95AC-F54F74E9A239", "796B6B5F-613C-4E24-A17C-EBA730D49C02", "8909E28E-5832-42F4-9886-B0A5545F3645", "2B3B8D2D-10AA-4BE4-B5FD-7F2FEB0C3091"],
            "isAddOn": true,
            "isAvailableForPurchase": true,
            "billing": "license",
            "isAutoRenewable": true,
            "salesGroupId": "1",
            "product": {
                "id": "90A8F363-DA30-4ECD-90A7-D3A6B203486D",
                "name": "Microsoft MyAnalytics",
                "unit": "Licenses"
            },
            "unitType": "Licenses",
            "links": {
                "learnMore": {
                    "method": "GET",
                    "headers": []
                },
                "self": {
                    "uri": "/offers/45320EC9-9B8E-49D0-B900-F14141A0ABD1?country=US",
                    "method": "GET",
                    "headers": []
                }
            },
            "attributes": {
                "objectType": "Offer"
            }
        }
    ],
    "attributes": {
        "objectType": "Collection"
    }
}
```
